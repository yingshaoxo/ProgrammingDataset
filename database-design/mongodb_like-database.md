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

* method 1: add '#' symbol at the begnning of a line to indicate it is a deleted line
* method 2: add '{"deleted": true}' in the json object of that line to indicate it is a deleted record

## Edit

One way is to delete the old line of record, and add a new one at the bottom of that \`database.txt\` file.

Another way is to use bytes seek tech, I could show you in code:

```python
def edit_record(database_file, record_id, field_name, new_value):
  """
  Edits the record with the given ID in the given database file.

  Args:
    database_file: The path to the database file.
    record_id: The ID of the record to edit.
    field_name: The name of the field to update.
    new_value: The new value for the field.

  Returns:
    None.
  """

  # Open the database file in read-write mode.
  # r+ means reading and writing the file.
  with open(database_file, "r+") as f:

    # Find the line that contains the record to edit.
    for line in f:
      if record_id in line:
        break

    # Seek to the beginning of the line that contains the record to edit.
    f.seek(f.tell() - len(line))

    # Update the value of the field in the record.
    line = line.replace(field_name, new_value)

    # Write the updated line back to the database file.
    f.write(line)
```

Or

```python
@yingshaoxo_version
def edit_record(database_file, record_id, field_name, new_value):
  """
  # Open the database file in text-read mode.
  with open(database_file, "r+") as f:
    last_position = None
    while True:
      current_position = f.tell()
      line = f.readline()
      
      if (last_position == current_position):
        # Reach the end of the file
        break
        
      last_position = current_position
          
      # Find the line that contains the record to edit.
      if record_id in line:
        break
        
    # Replace the field in the record with the new value.
    line = line.replace(field_name, new_value)
    
    # Go back the the begining of that record string
    f.seek(last_position)

    # Write the updated line back to the database file.
    f.write(line)
```

## For multi\_process usage

You can write a queue to handle those request. Which can make sure your database is safe under multi\_process usage.
