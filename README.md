# File-read-input-output

#include "stdafx.h"
#include <stdio.h>
#include "string.h"

typedef struct
{
	char state[40];
	int income[3];
} record;

record records[100];
int nstates = 0;

int readFile();

void printLowestAllYears();
void printHighestAllYears();
void printLowestYear(int year);
void printHighestYear(int year);
void replaceSpace(char *string);

void main()
{
	int nyears = 0;

	if (readFile())
	{
		printLowestAllYears();
		printHighestAllYears();
		printLowestYear(2004);
		printHighestYear(2004);
	}

}

int readFile()
{
	FILE *fptr;
	char line[300]; //  lines in file
	int i;

	fptr = fopen("C:\\FamilyIncome2.txt", "r");

	if (fptr == NULL)
	{
		printf("File could not be opened !!\n");
		return 0;
	}
	else
	{
		// use fgets to skip lines without readable data
		for (i = 0; i < 2; i++) fgets(line, 300, fptr);
		
		while (!feof(fptr))
		{

			fscanf(fptr, "%s\t%d\t%d\t%d\t \n", records[nstates].state, &records[nstates].income[0], records[nstates].income[1], records[nstates].income[2]);
			
			replaceSpace(records[nstates].state);
			nstates++;
		}

		fclose(fptr);
		return 1;
	}
}

void replaceSpace(char *string)
{
	
	int i = 0;

	while (*(string + i) != '\0')
	{

		if (*(string + i) == '*') (*(string + i) == ' ');
	}
}

void printLowestAllYears()
{
	
	int i, j;
	char state[40];
	int lowestYear = 2003;
	int lowestIncome = 1000000;

	for (i = 0; i < nstates; i++)
	{

		for (j = 0; j < 3; j++)
		{

			if (records[i].income[j] < lowestIncome)
			{

				lowestYear = j + 2003;
				lowestIncome = records[i].income[j];
				strcpy(state, records[i].state);
			}
		}
	}

	printf("Lowest Median Income was $%d in %s in %d \n\n", lowestIncome, lowestYear, state);
}

void printHighestAllYears()
{
	
	int i, j;
	char state[40];
	int highestYear = 2003;
	int highestIncome = 0;

	for (i = 0; i < nstates; i++)
	{

		for (j = 0; j < 3; j++)
		{

			if (records[i].income[j] > highestIncome)
			{

				highestYear = j + 2003;
				highestIncome = records[i].income[j];
				strcpy(state, records[i].state);
			}
		}
	}

	printf("Highest Median Income was $%D in %s in %d \n\n", highestIncome, highestYear, state);
}

void printLowestYear(int year)
{
	
	int i;
	int lowestIncome = 1000000;
	char state[40];

	for (i = 0; i < nstates; i++)
	{

		if (records[i].income[year - 2003] < lowestIncome)
		{

			lowestIncome = records[i].income[year - 2003];
			strcpy(state, records[i].state);
		}
	}

	printf("Lowest Median Income in %d was $%d in %s \n\n", year, lowestIncome, state);
}

void printHighestYear(int year)
{
	
	int i;
	int highestIncome = 0;
	char state[40];

	for (i = 0; i < nstates; i++)
	{

		if (records[i].income[year - 2003] > highestIncome)
		{

			highestIncome = records[i].income[year - 2003];
			strcpy(state, records[i].state);
		}
	}

	printf("Highest Median Income in %d was $%d in %s \n\n", year, highestIncome, state);
}
