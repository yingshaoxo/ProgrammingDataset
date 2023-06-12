# Mongodb\_Like Database

## Initiate

First, create a \`database.txt\` file.

Then, for each line, it is a json string. That json string is actually a dict.

## Add

When you add a record, you append a new json string at the bottom of that \`database.txt\` file.

## Search

When you search for a record, you iterate all those json string.

For each line of json string, you use a python function to handle it.

If a record is not what you want, you return None, if a record is what you want, you return a dict result.

In the end, you'll ignore those None result, and get a list of dict object.

```python
>>> import subprocess
>>> pycode = """
... import sys
... if sys.argv[1] == 'nice_guy':
...     print('yingshaoxo')
... else:
...     print('unrecognized arg')
... """

>>> result = subprocess.run(['python', '-c', pycode, 'nice_guy'], stdout=subprocess.PIPE)
>>> print(result.stdout.decode())
yingshaoxo
```

## Delete

I do not recommend do the real deletion for a line of json string when other process is reading that file.

I would recommend you to use some special tech to do it:

Add '#' symbol at the begnning of a line to indicate it is a deleted line.

> You can do it by replace the first character of a line with '#' symbol

## Edit

Simply delete the old line of record, and add a new one at the bottom of that \`database.txt\` file.

Another way is to use bytes seek tech, but it is limitations, it can only be used on limit size record data, in other words, every row should have same length:

```python
def delete(self, one_row_dict_filter: Callable[[dict[str, Any]], bool]):
    """
    one_row_dict_filter: a_function to handle deletion process. If it returns False, we'll ignore it, otherwise, if it is True, we'll delete that row of data.
    """
    with open(self.database_txt_file_path, "r+") as file_stream:
        end_detection_counting = 1
        old_position_pair = None
        while True:
            previous_position = file_stream.tell()
            line = file_stream.readline()
            current_position = file_stream.tell()

            new_position_pair = (previous_position, current_position)
            #print(new_position_pair)
            if old_position_pair == new_position_pair:
                end_detection_counting += 1 
            else:
                old_position_pair = new_position_pair
            if end_detection_counting >= 3:
                # We could make sure it is the end of the file
                old_position_pair = None
                break

            if (line.strip() == ""):
                # ignore empty line
                continue

            json_dict = self._json.loads(line)
            result = one_row_dict_filter(json_dict)
            #print(result)
            if (result == True):
                # replace the old line into space
                file_stream.seek(previous_position)
                file_stream.write((" "*(len(line)-1)) + "\n")
```

## For multi\_process usage

You can write a queue to handle those request. Which can make sure your database is safe under multi\_process usage.

## For extreme long and big string situation

We can set variable limit = 255

If any fieid in a dict has value length > 255, then we add '{"\*-\*use\_additional\_space": true}' and '{"\*-\*additional\_json\_path": "./random\_hash.json"}' to that record.

Then we put the original json record into that additional\_json file without deleting any big value.

But for the record in 'database.txt', we simply set all field value that > 255 to null. (It is to speed up the search speed)

And when we do searching, or any other operations, we simply load that additional\_json file into memory, then everything works as usual.
