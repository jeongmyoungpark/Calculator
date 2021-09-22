@@ -0,0 +1,392 @@
#include <stdio.h>
#include <stdlib.h>
#pragma warning(disable : 4996)
#define SIZE 100

//식 받아서 파싱후 스택에 집어넣기.(후위)
//int top = -1;
char num[100];
//char stack[SIZE];
//float intstack[SIZE];
char spec_a[100];
char spec_b[100];

typedef struct Node
{
	char op;
	struct Node* link;
}Node;
Node* top1;

typedef struct InNode
{
	float num;
	struct InNode* link;
}InNode;

//
int isempty() {
	if (top1 == NULL) {
		return 1;
	}
	return 0;
}

void push(char op1) {
	Node* newnode = (Node*)malloc(sizeof(Node));
	newnode->op = op1;
	newnode->link = top1;

	top1 = newnode;
}

void pushing(float number) {
	InNode* newnode = (Node*)malloc(sizeof(Node));
	newnode->num = number;
	newnode->link = top1;

	top1 = newnode;
}

char pop() {
	if (!isempty()) {
		Node* temp = top1;
		char op1 = temp->op;
		top1 = temp->link;
		free(temp);

		return op1;
	}
}

float popping() {
	if (!isempty()) {
		InNode* temp = top1;
		float number = temp->num;
		top1 = temp->link;
		free(temp);

		return number;
	}
}
char peek() {
	if (!isempty()) {
		return top1->op;
	}
}
int prec(char op) {
	switch (op)
	{
	case '(': case')':
		return 0;
	case '+': case'-':
		return 1;
	case '*': case'/':
		return 2;
	}
	return -1;
}
//

/*
int IsEmpty() {
	if (top < 0)
		return 1;
	else
		return 0;
}
int IsFull() {
	if (top >= SIZE - 1)
		return 1;
	else
		return 0;
}

void push(char data) {
	if (!IsFull()) {
		top++;
		stack[top] = data;
	}
}

void pushing(float data) {
	if (!IsFull()) {
		top++;
		intstack[top] = data;
	}
}


void pop() {
	if (!IsEmpty()) {
		stack[top--];
	}
}


void delete() {
	if (!IsEmpty()) {
		for (int i = 0; i < 50; i++)
			pop();
	}
}
*/

int count = 0;

void post() {
	char a;
	int prior = -1;
	int flag = 0; //괄호 다음 마이너스

	int flag2 = 0;//처음 마이너스
	
	int flag3 = 0; //괄호 - 괄호
	int flag4 = 0;
	int flag5 = 0;

	for (int i = 0; i < 100; i++) {
		
		if (num[i] >= '0' && num[i] <= '9')
		{
			//1번 숫자는 배열에 넣습니다.
			spec_a[count++] = num[i];
			flag = 0;
			flag2 =1;
			flag3 = 0;
		}
		else if (num[i] == '+' || num[i] == '-' || num[i] == '*' || num[i] == '/') {
			
			spec_a[count++] = ','; //띄어쓰기를 위함
			// 우선순위 (,)=0     +,-=1     /,*=2
			if (num[i]=='-')
				flag4 = 1;
			else
			{
				flag4 = 0;
			}
			

			//printf('%d', prec(peek()));
			//우선순위가 낮은 기호 top일때 top-1출력
			
				if (peek() != NULL)
					prior = prec(peek());
				if (prec(num[i]) <= prior)
				{
					spec_a[count++] = pop();
					spec_a[count++] = ','; //띄어쓰기를 위함

					if (peek() != NULL)
						prior = prec(peek());
					if (prec(num[i]) <= prior)
					{
						spec_a[count++] = pop();
						spec_a[count++] = ','; //띄어쓰기를 위함

						if (peek() != NULL)
							prior = prec(peek());
						if (prec(num[i]) <= prior)
						{
							spec_a[count++] = pop();
							spec_a[count++] = ','; //띄어쓰기를 위함

							if (peek() != NULL)
								prior = prec(peek());
						}
					}
				}
		
			push(num[i]);//2번 스택에 기호를 넣는다

			if ((num[i] == '-') && flag2 == 0) {
				spec_a[count++] = '0';  //문자 -1추가
				spec_a[count++] = ',';  //문자 사이추가
			}


			//prior= top-1값
			
			prior = prec(num[i]);
			
			if (flag == 1 && num[i] == '-') {
				flag = 0;
				spec_a[count++] = '`';  //문자 -1추가
				pop();
			}
			

		}

		else if (num[i] == '(') {
			flag = 1;
			flag5 = 1;
			if (flag3 == 1 && flag4 == 1 && flag5==1) {
				spec_a[count++] = '0';  //문자 -1추가
				spec_a[count++] = ',';  //문자 -1추가
				push('-');
			}
			else
			{
				flag3 = 0;
				flag4 = 0;
			}
			flag3 = 1;
			push(num[i]);
			

		}
		else if (num[i] == ')') {
			spec_a[count++] = ','; //띄어쓰기를 위함
			a = pop();
			while (a != '(') {
				spec_a[count++] = a;
				a=pop();
				spec_a[count++] = ','; //띄어쓰기를 위함
			}
			
		}
	}
	//높은기호가없어서 탑부터 마지막 배열에 넣어준다.
	spec_a[count++] = ','; //띄어쓰기를 위함

	for (int i = 0; i < 20; i++) {
		spec_a[count++] = pop();
	}

	printf("후위로 바꾼 식 : ");
	for (int i = 0; i < count; i++)
	{
		printf("%c", spec_a[i]);
	}
}

void cal() {//후위받아서 계산하기!!!!!!!
	float sum = 0; //float
	float n = 0; //float
	float a, b; //float
	int cc = 0;
	int minus_ch = 0;
	post();

	//char->int
	for (int i = 0; i < 100; i++) {
		
		if (spec_a[i] == '`') {
			minus_ch = 1;
		}
		
		if (spec_a[i] >= '0' && spec_a[i] <= '9')
		{
			spec_b[cc++] = spec_a[i];
		}
		else if (spec_a[i] == ',')
		{
			if (cc == 4)
			{
				n = ((spec_b[cc - 4] - 48) * 1000) + ((spec_b[cc - 3] - 48) * 100) + ((spec_b[cc - 2] - 48) * 10) + (spec_b[cc - 1] - 48);
				//printf("n은 : %d", n);

				if (minus_ch == 1)
				{
					pushing(-1 * n);
					minus_ch = 0;
				}
				else
				{
					pushing(n);
				}
			}
			if (cc == 3)
			{
				n = ((spec_b[cc - 3] - 48) * 100) + ((spec_b[cc - 2] - 48) * 10) + (spec_b[cc - 1] - 48);
				//printf("n은 : %d", n);


				if (minus_ch == 1)
				{
					pushing(-1 * n);
					minus_ch = 0;
				}
				else
				{
					pushing(n);
				}
			}
			else if (cc == 2)
			{
				n = ((spec_b[cc - 2] - 48) * 10) + (spec_b[cc - 1] - 48);
				//printf("n은 : %d", n);


				if (minus_ch == 1)
				{
					pushing(-1 * n);
					minus_ch = 0;
				}
				else
				{
					pushing(n);
				}
			}
			else if (cc == 1) {
				n = spec_b[cc - 1] - 48;
				//printf("n은 : %d", n);


				if (minus_ch == 1)
				{
					pushing(-1 * n);
					minus_ch = 0;
				}
				else
				{
					pushing(n);
				}
			}
			cc = 0;
		}
		else if (spec_a[i] == '+' || spec_a[i] == '-' || spec_a[i] == '*' || spec_a[i] == '/')
		{
			cc = 0;
			b = popping();
			a = popping();


			if (spec_a[i] == '+') {
				sum = a + b;

				printf("\n%f %c %f  :  %f\n", a, spec_a[i], b, sum);
				pushing(sum);
			}
			else if (spec_a[i] == '-') {
				sum = a - b;
				printf("\n%f %c %f  :  %f\n", a, spec_a[i], b, sum);

				pushing(sum);
			}
			else if (spec_a[i] == '*') {
				sum = a * b;
				printf("\n%f %c %f :  %f\n", a, spec_a[i], b, sum);

				pushing(sum);
			}
			else if (spec_a[i] == '/') {
				sum = a / b;
				printf("\n%f %c %f :   %f\n", a, spec_a[i], b, sum);

				pushing(sum);
			}
		}
	}
	printf("top결과 : %f", popping());
}
int main()
{


	printf("식을 입력하세요 : ");
	scanf("%s", num);
	//post();
	cal();
}
