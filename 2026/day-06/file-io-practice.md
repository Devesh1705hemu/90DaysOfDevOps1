# Linux Fundamentals: Read and Write Text Files

______________________________________________________________________________

# Use: Creates an empty file
touch notes.txt
________________________________________________________________
# Use: Writes text into file and overwrites old content
echo "Linux practice Day 06" > notes.txt

____________________________________________________________
# Use: Appends text into existing file
echo "Learning file operations" >> notes.txt
___________________________________________________________________________
# Use: Displays output and appends it into file simultaneously
echo "Using tee command" | tee -a notes.txt

__________________________________________________________________________________________
# Use: Appends another line into file
echo "Reading files is important" >> notes.txt

________________________________________________________________________________
# Use: Adds line into file
echo "head shows starting lines" >> notes.txt

____________________________________________________________________________
# Use: Adds line into file
echo "tail shows ending lines" >> notes.txt

________________________________________________________________________
# Use: Adds line into file
echo "Linux commands improve skills" >> notes.txt

______________________________________________________________________________
# Use: Adds line into file
echo "Practice daily for consistency" >> notes.txt

_____________________________________________________________________________________
# Use: Displays full file content
cat notes.txt

_____________________________________________________________________________________---
# Use: Shows first 2 lines of file
head -n 2 notes.txt

# Use: Shows last 2 lines of file
tail -n 2 notes.txt
