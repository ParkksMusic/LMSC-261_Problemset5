# Problem Set 5

Start Date and Time| Due Date and Time | Cut-off Date and Time |
---|---|---|
10:50:00 AM on October 11, 2019 | 11:59:59 PM on October 22, 2019 | 12:00:00 AM on October 30, 2019 |

## Recommended Reading 
- [Sorting Algorithms Animations](https://www.toptal.com/developers/sorting-algorithms)
- [15 Sorting Algorithms in 6 Minutes](https://www.youtube.com/watch?v=kPRA0W1kECg)

## Problem 5.1: N-Grams
### Introduction
[N-gram](https://en.wikipedia.org/wiki/N-gram) is all combinations of adjacent *letters* of length `n` that we can find in a text file. N-gram of texts is extensively used in [text mining](https://en.wikipedia.org/wiki/Text_mining), [natural language processing](https://en.wikipedia.org/wiki/Natural_language_processing), and [genetic sequence analysis](https://en.wikipedia.org/wiki/Sequence_analysis) tasks.

If our analysis string is `"I love you"` and we set the value of `n` to 3, we can create a trigram sequence that looks like this (double quotes are there for clarity):

- "I l"
- " lo"
- "lov"
- "ove"
- "ve "
- "e y"
- " yo"
- "you"

The basic point of n-grams is to capture the language structure from the statistical point of view, such as what *letter* or *word* is likely to follow the given one. The longer the n-gram (the higher the `n`), the more context you have to work with. The optimum length depends on the application: if your n-grams are too short, you may fail to capture essential differences. On the other hand, if they are too long, you may fail to capture the "general knowledge" and only stick to particular cases.

One of the most popular applications of the n-gram algorithm is the [Google Books Ngram Viewer](https://books.google.com/ngrams). The viewer allows us to enter a list of phrases and then displays a graph showing how often the phrases have occurred in a large corpus of books (e.g., "British English", "English Fiction", "French") over time. Try keywords like "hipster", "disco", and "funky" to find out the number of times they have been used in over 5 million books. 

### Objective
Implement a C program that creates n-grams and save them in a text file named `Ngram.txt`. The program should take one additional argument from the user that specifies the size of `n`. The program should also open the `LoremIpsum.txt` file and read characters in the text using the `fgetc()` function. A template c file named `ProblemSet5.1.c` is provided for you as a starting point that implements all of the above functionality. 

You task is to write two functions to complete this problem. The first function is `appendCharacter()`. The function prototype is:

    void appendCharacter(int n, char chr, char chrs[]);

`appendCharacter()` takes three arguments: `n`, the size of n-gram; `chr`, a character to be appended; and `chrs` that holds n-gram letters. This function should shift previous `n - 1` characters in `chrs` to make space for the new character `chr`. This means the oldest character in `chr` gets thrown away when this operation completes. The function should then append `chr` into `chrs`. 

The second function to implement is `saveNgram()`. The function prototype is: 

    void saveNgram(int n, char chrs[], FILE *file);

`saveNgram()` takes three arguments: `n`, the size of n-gram; `chrs` that holds n-gram letters; and `file`, a text file to write all n-grams. In this function, go through each character and write them into the file using the `fputc()` function. Terminate each n-gram with `\n` so that each new line in the text file represents an n-gram. Here is a few lines of texts from `Ngram.txt` file when the user inputs `4` to be the value of `n`:

    Veri
    erit
    rita
    itat
    tati
    atis

When the user inputs `2` to be the value of `n`, the first few lines of `Ngram.txt` file should look like this:

    Ve
    er
    ri
    ie
    er
    ri
    ir

## Problem 5.2: Bubble Sort
This problem focuses on sorting the n-grams that you created and saved. A template file named `ProblemSet5.2.c` is provided for you as a starting point for this problem. Your task is to implement the `sort()` function. The function prototype for `sort()` is:

    void sort(char arr[MAX_ARRAY_SIZE][SIZE], int size);

`sort()` takes an array of strings named `arr` that holds all n-grams read from the `Ngram.txt` file. `MAX_ARRAY_SIZE` is arbitrarily set to `196605` to make sure we can hold all n-grams (strings) in the array. `SIZE` is for the size of each string. Since the maximum number of `n` was set to `32` in the previous problem, we can safely assume that each n-gram will never be longer than `32` when we read them from the text file. `sort()` also takes `size` variable which holds the number of n-grams read from the text file.

Implement the [bubble sort](https://en.wikipedia.org/wiki/Bubble_sort) inside `sort()`. Since we are dealing with an array of strings, the [`strcmp()`](http://www.cplusplus.com/reference/cstring/strcmp/) and [`strcpy()`](http://www.cplusplus.com/reference/cstring/strcpy/?kw=strcpy) functions from [`string.h`](http://www.cplusplus.com/reference/cstring/) must be used in comparing and swapping strings in your bubble sort algorithm. The `strcmp()` function is for comparing two strings. The result of comparison indicates the relationship between the strings (`<0`, `0`, or `>0`). `strcpy()` is for copying one string to another string. Pay attention to the source and destination strings when copying strings using `strcpy()`. You will also need a temporary variable for swapping strings, declare your variable as an array (e.g. `char tmp[SIZE]`) and not as a pointer (e.g. `char *tmp`). Do not use the `malloc()` function for this problem.

Print out the result of sorting to complete this problem. Here is an example output on CLI when `4` was the value of `n` in the previous problem (appears in 3 characters but there is leading whitespace in the output):

     Con
     Cup
     Dol
     Duc
     Duc

## Problem 5.3: Count N-Gram Frequency
Counting n-grams is an essential part of language models, which perform an essential role in machine translation, speech recognition, optical character recognition, spelling correction, and text input method. Since we sorted our n-grams in the last problem, it is much easier for us to be able to count how many times each n-gram occurred in a text file. It is easier because we know that the n-grams with the same letter sequence will be side by side in the sorted array. We can iterate over the sorted array and count the number of occurrences if the current n-gram sequence is the same as the previous n-gram sequence.

A template for this problem is provided in `ProblemSet5.3.c`. Your task is to implement the `countUniqueItems()` function. The function prototype is:

    void countUniqueItems(int n, char ngram[MAX_ARRAY_SIZE][SIZE]);

`countUniqueItems()` takes two arguments. The variable `n` represents the size of n-grams read from the `Ngram.txt` file. The `ngram` variable holds the sorted n-grams from the previous problem. Count the number of occurrences for each n-gram and print them out in the `countUniqueItems()` function. Use the `strcmp` and `strcpy` functions from `string.h` for this problem. 

When printing out the frequency count, the output should look like this:

     Con -> 1
     Cup -> 1
     Dol -> 1
     Duc -> 2

The left side of `->` is the actual n-gram, while the numbers on the right side represents the frequency count of that n-gram in the text file.

## Grading Rubric
Description|Grade
---|---:|
Submitted all programs.|10%
No compilation warning or error on all programs.| 10%
Programs are clean, understandable, commented and organized. | 10%
Thoroughly documented in *README.md* what the programs do. | 20%
Correctly implemented all programs.| 50%
**Total** | **100%**

## Submission Guideline
- Create a new GitHub project with the right name and problem set number (e.g., `LMSC261-ProblemSet1`).
- Commit and push Scratch files for this problem set into the newly created project.
- Submit the link to the repository on OL to complete the problem set.

## Submission policy:
- All problem set must be first committed and pushed to your GitHub repository. 
- The link to your repository must be submitted to OL to complete the problem set.
- Late projects will incur a penalty of 10% each day.
- Problem sets and projects are due by 11:59:59 pm on the date specified
- After 12:00:00 am (the next day after the due day), your problem sets/projects is one day late (-10%).
- After the next 12: 00:00 am cycle (two days after the due day), your problem sets/projects is two days late (-20%).
- Problem sets and projects will not be accepted after 12:00:00 am at one week after the deadline

---  
**Berklee College of Music**    
Liberal Arts Department  
LMSC-261: Introduction to Computer Programming  
Fall 2019