# Mongodb\_Like Database (Version 2)

## Initiate

First, create a folder called \`database\`

Then, create a `yingshaoxo_database_index.txt` file under that database folder.

For each line, we'll put a relative\_path towards a json\_file that under some sub\_folders like './1/current\_index\_row\_number\_plus\_random\_hash\_string.json'

## Add

When you add a record, you first read how many lines the \`yingshaoxo\_database\_index.txt\` has, let's say, index\_length = 11

Then you create a json file that has the new data with a name of '11\_random\_hash\_string.json'

After that, you append that json path at the bottom of \`yingshaoxo\_database\_index.txt\` file.

> For windows system, it can't have more than 4,294,967,295 files under a folder.&#x20;
>
> So you'd better seperate files into different folders.

## Search

When you search for a record, you iterate all those json path inside \`yingshaoxo\_database\_index.txt\`.

You read each json object. For each json object, you use a python function to handle it.

If a record is not what you want, you return None, if a record is what you want, you return a dict result.

In the end, you'll ignore those None result, and get a list of dict object.

## Delete

I do not recommend you to do the real deletion when other process is reading that file.

I would recommend you to use some special tech to do it:

Add '#' symbol at the begnning of a json path to indicate it is a deleted json object.

> You can achive this by replacing the first chracter of the path with '#' symbol

## Edit

The edit can be as simple as replace the old json data with the new one.

## For multi\_process usage

You can write a queue to handle those request. Which can make sure your database is safe under multi\_process usage.

## Null safety

When you change data\_stucture, how to make sure everything is OK?

For old data, in the view of new data\_stucture, for those fields that missing data, you replace it with null.

