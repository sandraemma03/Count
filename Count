#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct words
{
	char *word;		//struct words is a binary tree that stores a node and a pointer to the left and right siblings
	int count;
	struct words *left;
	struct words *right;
};

struct words *bintree(struct words **head,char *word);   //bintree is a function of type struct words and the 1st arg is a                                                        pointer to the bin tree that stores the words

void print_tree(struct words *head);              //print_tree is a function that prints a binary tree
char *readfile(char *complete);                   //readfile is a function that reads a text file and stores it in a string
int total;                                        //an interger to store the total number of words in the file
                                              
int main (int argc, char *argv[])
{
	char *word=NULL,*str=NULL;
	total = 0;
	struct words *head=NULL;
	
	if((str = readfile(argv[1])) != NULL)
	{		
		const char* delim = 
            " ,\n\r\t.;:_-()~`|!?><%^&*$#@{}[]0123456789\'\"/";     //delim is list of all characters that seperates two                                                                 words form each other

		word = strtok(str,delim);               //strtok is takes a string and seperates it into words using the delimities 
		head = bintree(&head,word);
		while((word = strtok(NULL,delim)) != NULL)
        {
			head = bintree(&head,word);
		}
		printf("Total = %d\n\n",total);
		printf("|%-20s | %-5s | \n%28s\n","WORDS","freq", "===============================");
		print_tree(head);
	}
	return 0;
}

void print_tree(struct words *head)
{
	if(head == NULL)
		return ;
	print_tree(head->right);                    //print_tree uses the post order traversal to print the tree
	printf("|%-20s | %-5d |\n",head->word,head->count);
	print_tree(head->left);
	return ;	
}

char *readfile(char *complete)
{
	FILE *fp = fopen(complete,"r");
	char *str=NULL;
	if(fp !=NULL)
    {
		fseek(fp,0,SEEK_END);                   //moves the pointer 2 the end of the file
		long int size = ftell(fp);              //ftel determine the size of the file
		rewind(fp);                             //rewind brings the pointer back to te beginning
		str = malloc(size + 1);
		fread(str,size,1,fp);                   //fread read the the entire file and stores it in a file.the 1 signifies it                                                is reading the entire file as one block
		fclose(fp);
	}
	return str;
}

struct words *bintree(struct words **head,char *word)
{
	if(*head == NULL)
    {
		*head = malloc(sizeof(struct words *));
		(*head)->word = malloc(sizeof(char) * strlen(word) + 1);
		strcpy((*head)->word,word);
		(*head)->count = 1;
		(*head)->left = (*head)->right = NULL;
		total++;
	}
	else if(strcasecmp((*head)->word,word) < 0)       //strcasecmp compares strings without considering the cases of string
    {
		bintree(&(*head)->left,word);                 
	}
	else if(strcasecmp((*head)->word,word) > 0){
		bintree(&(*head)->right,word);
	}
	else{
		(*head)->count++;
		total++;
	}
	
	return *head;
} 
