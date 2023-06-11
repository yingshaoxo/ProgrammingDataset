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

## Delete

I do not recommend do the real deletion for a line of json string when other process is reading that file.

I would recommend you to use some special tech to do it:

* method 1: add '#' symbol at the begnning of a line to indicate it is a deleted line
* method 2: add '{"deleted": true}' in the json object of that line to indicate it is a deleted record

## Edit

One way is to delete the old line of record, and add a new one at the bottom of that \`database.txt\` file.

Another way is what???

