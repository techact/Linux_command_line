

sed '/PATTERN/q' FILE

It works like this:

For each line, we look if it matches /PATTERN:

    if yes, we print it and quit
    otherwise, we print it

This is the most efficient solution, because as soon as it sees PATTERN, it quits. Without q, sed would continue to read the rest of the file, and do nothing with it. For big files it can make a difference.

This trick can also be used to emulate head:

sed 10q FILE




print up to and including the match:

awk '{print} /pattern/ {exit}' filename
sed '/pattern/q' filename

print up to BUT NOT including the match:

awk '/pattern/ {exit} {print}' filename
sed '/pattern/Q' filename



sed can replace most of grep's functionality.

sed -n '1,/<pattern>/ p' <file>

This means print from the first line until pattern is matched.

A couple of range examples

sed -n '/<pattern>/,$ p' <file> # from pattern to end of file
sed -n '/<pattern1>/,/<pattern2>/ p' <file> # from pattern1 to pattern2

The following pure GNU grep methods are not efficient.

Search for everything up to the first instance of string "foo" in file bar, using three greps:

grep -m 1 -B $(grep -n -m 1 foo bar | grep -o '^[0-9]*') foo bar

Matching up to the last instance of "foo":

grep -oPz "(?s)[^\n]*${s}.*?\n.*?foo.*?\n" bar

