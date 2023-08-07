# Building Bash Scripts

## Using Shell Logic and Control Flow

Logic guided by **conditional statements** to handle events so you can fully automate a pipeline or a workflow.

#### Example
```
#!/bin/sh
echo "What food do you choose? "
read FOOD

if [ "$FOOD" = "Apple" ]; then
  echo "Eat Yogurt with your Apple"
elif [ "$FOOD" = "Milk" ]; then
  echo "Eat Cereal with your Milk."
else
  echo "Eat your ${FOOD} by itself!"
fi
```

You need to make this script executable:

```
chmod +x <file-name>
```

### Using Shell Loops in Bash

#### Examples
```
#!/usr/bin/env bash
declare -a array=("apple" "pear" "cherry")

## now loop through the above array
for i in "${array[@]}"
do
  echo "This ${i} is delicious!"
done

```
```
#!/usr/bin/env bash

echo "How Many loops do you want?"
read LOOPS

COUNT=1
while [ $COUNT -le $LOOPS ]
do
  echo "Loop# $COUNT "
  ((COUNT++))
done
```

### Evaluating Conditions

- **AND** operator: &&
- **OR** operator: ||

```
#!/usr/bin/env bash

touch one.txt\
  && touch two.txt\
  && touch three.txt\

  #count the files created
  ls *.txt | wc -l

```

## Manipulating Data with the Shell

### Truncating Data in Bash

```
head -n 2 file.txt
tail file.txt

# get 3 random lines from this file
shuf -n 3 file.txt
```
### Filtering Data in Bash

- **grep**: find a pattern in the files, such as the word "bird"

```
# Return all lines that contains "apple"
grep apple filter-file.txt

# Count the number of occurances
grep -c apple filter-file.txt

# Search for more than one pattern
grep -e apple -e pear filter-file.txt
```

Principais opções **Grep**:
  - -i: Ignora diferenças entre maiúsculas e minúsculas.
  - -v: Inverte a busca, ou seja, mostra as linhas que não correspondem ao padrão.
  - -r ou -R: Faz uma busca recursiva em diretórios e subdiretórios.
  - -l: Mostra apenas o nome dos arquivos que contêm o padrão.
  - -n: Mostra o número da linha juntamente com a linha correspondente.
  - -c: Mostra o número total de linhas que correspondem ao padrão.
  - -E ou --extended-regexp: Permite o uso de expressões regulares estendidas.
  - -F ou --fixed-strings: Trata o padrão como uma string literal, não uma expressão regular.
  - -e: Essa opção é usada para especificar explicitamente o padrão de pesquisa que você deseja usar.
Pode ser útil quando o padrão começa com um hífen -, para evitar que o grep interprete o padrão como uma opção.
Pode ser usado para procurar diversas ocorrências no mesmo comando.

### Searching Data in Bash

```
# Dot - current directory
find . -name "*.sh"

# find all excutable non-invisible files (! -name '.*' sets for not invisible)
find . -perm /+x ! -name '.*' -type f

# find all executable non-invisible files and ignore .git directories
0
```

## Writing Bash Scripts and Command-Line Toos

### Building Scripts in Bash

Tells the script which environment it should use:
#!/usr/bin/env bash

"Though comments are of little use on the command line, they will work.
The first line of our script is a little mysterious. It looks as if it should be a comment since
it starts with #, but it looks too purposeful to be just that. The #! character sequence is,
in fact, a special construct called a shebang. The shebang is used to tell the kernel the
name of the interpreter that should be used to execute the script that follows. Every shell
script should include this as its first line."

```
# Set strict mode. Causes shell to exit when a command fails
set -e

# Enables printing of shell input lines as they are read
set -v

# Enables print of command traces before executing command
set -x
```
The next thing we have to do is make our script executable. This is easily done using chmod.


### Building a Bash Function

```
mimic() {
  echo "First Parameter: $1"
  echo "Second Parameter: $2"
}

# Calling the function
mimic 1 2

add() {
  num1=$1
  num2=$2
  result=$((num1 + num2))
  echo $result
}

```

### Command-Line Tools

```
## A. Does the work
# Generate phrases "N" times

phrase_generator() {
    for ((i=0; i<$1;i++)); do
        echo "$2"
    done
}

## B. Parses input from the CLI
# Parse Options
while [[ $# -gt 1 ]]
do
key="$1"

case $key in
    -c|--count)
    COUNT="$2"
    shift
    ;;
    -p|--phrase)
    PHRASE="$2"
    shift
    ;;
esac
shift
done

## C. Pass parsed input to a function and run everything
# Run program
phrase_generator "${COUNT}" "${PHRASE}"
```
