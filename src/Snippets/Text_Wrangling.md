# Text Wrangling

# grep

## Find & Print IP Addresses:

```bash
grep -REo '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}'

grep -RPo '\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3}'
```

## Grep OR (e.g. A or B or C or D)

`grep 'A\|B\|C\|D'`

## Grep AND (e.g. A and B)

`grep 'A.*B'`

## Regex any single character (e.g. ACB or AEB)

`grep 'A.B'`

## Grep for a Tab White Space:

`grep $'\t'`

## Grep between brackets:

`grep -oP '\(\K[^\)]+'`

-----

# sed

## Remove First Line:

`sed 1d filename`

## Remove first 100 lines:

`sed 1,100d filename`

## Remove all lines containing $STRING:

`sed "/$STRING/d" filename`

## case insensitive:

`sed "/$STRING/Id" filename`

OR

`sed -i "/$STRING/d" filename`


## Remove Empty Lines:

`sed '/^\s*$/d'`


OR


`sed '/^$/d'`


## Add String to beginning of file:

`sed -i '1s/^/[/' file`

## Add String to certain line numbers:

`sed -e '1isomething -e '3isomething'`

## Add String to EOF:

`sed '$s/$/]/' filename`

`sed -e 's/^/bbo/' file`

## Add string to end of each line (e.g. “}”)

`sed -e 's/$/\}\]/' filename`

## Add \n every nth character (e.g. every 4th character)

`sed 's/.\{4\}/&\n/g'`

## Concatenate/combine/join files with a seperator and next line (e.g separate by “,”)

`sed -s '$a,' *.json > all.json`

## Substitution (e.g. replace A by B)

`sed 's/A/B/g' filename`

## Remove newline\ nextline

`sed ':a;N;$!ba;s/\n//g'`

## Print a particular line (e.g. 123th line)

`sed -n -e '123p'`

## Print a number of lines (e.g. line 10th to line 33 rd)

`sed -n '10,33p' <filename`

## Change delimiter

`sed 's=/=\\/=g'`
