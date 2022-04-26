#!/bin/sh

# Recieve cut marks
if [ -z $2 ]; then
	TIMES=$(mktemp)
	INPUT='null'
	echo "Enter timestamps:"
	while [ -n "$INPUT" ] && [ "$INPUT" != "done" ]
	do
		read INPUT
		if [ -n "$INPUT" ] && [ "$INPUT" != "done" ]
		then
			echo "$INPUT" >> $TIMES
		fi
	done
else
	TIMES="$2"
fi

ext=${1##*.} # Grabbing video file extension

CAT=$(mktemp)

while read x && read y
do
	X=$(echo $x | sed s/://g)
	ffmpeg -i $1 -ss $x -to $y -c copy $X.$ext
	echo "file $(pwd)/$X.$ext" >> $CAT
done < $TIMES

# Concatenate

ffmpeg -f concat -safe 0 -i $CAT -c copy output.$ext
