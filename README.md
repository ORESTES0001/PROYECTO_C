# PROYECTO_C
PROYECTO DE C UNIVERSITARIO 2DO AÑO
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definir una estructura de productos
typedef struct sp
{
	
	char no[12];     //Número de producto
	char name[40];   //nombre
	char FechaVencimiento[40];   //nombre
	char Medidaaaa[40];   //nombre
	char descripcion[500];//descripcion
	int workload;    //inventario
	struct sp *next; // Puntero al siguiente nodo
} SP;

// La declaración de la función está aquí
void ListCreate(SP *L, int n); // Cree un nodo de lista vinculada a productos básicos
void LIstSearch(SP *L);        // Encuentra información sobre el producto
void ListModify(SP *L);        // Modificar la información del producto
void ListInsert(SP *L);        // Insertar información del producto
void ListDelete(SP *L);        // Eliminar información del producto
void Input(SP *p, int i);      // Ingrese la información del producto
void SumSp(SP *L);             // Estadísticas del inventario total de bienes
void Sort(SP *L);              // Clasifica el inventario de cada categoría
void Menu();                   // Menú del sistema de gestión de registro de exámenes

// La entrada de función principal del sistema de gestión de inventario de productos básicos
int main()
{
	int item, n;                  // el elemento se usa para recibir comandos de entrada, n se usa para recibir el número de elementos ingresados
	SP *L = NULL;                 // Inicializar un nodo principal
	L = (SP *)malloc(sizeof(SP)); // Abre espacio de memoria para el nodo principal
	L->next = NULL;               // Vacía el campo de puntero del nodo principal
	do
	{
		Menu(); //menú
		printf("Por favor ingrese el número correspondiente para realizar la operación correspondiente: \n");
		scanf("%d", &item);
		system("cls");
		switch (item)
		{
		case 1:
			printf("Ingrese el número de productos que desea ingresar:");
			scanf("%d", &n);
			ListCreate(L, n); 
			getchar();
			printf("\n Pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 2:
			LIstSearch(L); // Encuentra información sobre el producto
			getchar();
			printf("\n pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 3:
			ListModify(L); // Modificar la información del inventario de productos
			getchar();
			printf("\n Pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 4:
			ListDelete(L); // Eliminar información del producto
			getchar();
			printf("\n Pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 5:
			ListInsert(L); // Insertar información del producto
			getchar();
			printf("\n Pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 6:
			SumSp(L);
			getchar();
			printf("\n Pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 7:
			Sort(L);
			getchar();
			printf("\n Pulse cualquier tecla para volver al menú principal \n");
			getchar();
			system("cls");
			break;
		case 0: // Salir del sistema de gestión de inventario de productos básicos
			printf("El sistema de gestión de inventario de productos básicos se retirará pronto ...");
			exit(0);
		default:
			printf("La instrucción que ingresó es incorrecta, vuelva a ingresar");
		}
		printf("\n\n");
	} while (item);
	return 0;
}

// Cree una lista vinculada, inserte el nodo recién generado en el encabezado de la lista vinculada
void ListCreate(SP *L, int n)
{
	int i;
	for (i = 0; i < n; i++)
	{
		SP *p;
		// Inserta el nodo recién generado en la lista vinculada
		p = NULL;
		p = (SP *)malloc(sizeof(SP));
		Input(p, i);
		p->next = L->next;
		L->next = p;
	}
	printf("¡La entrada es exitosa!");
}

// Encontrar inventario de productos
void LIstSearch(SP *L)
{
	char n[40];
	SP *p = L->next;
	if (p == NULL)
		printf("¡Los datos están vacíos y no se pueden encontrar!");
	else
	{
		printf("Introduzca el nombre del producto que está buscando:");
		scanf("%s", n);
		while (strcmp(p->name, n) != 0)
		{
			p = p->next;
			if (p == NULL)
			{
				printf("No se encontró información relevante \n");
				return;
			}
		}
		printf("El inventario de % s es %d  \n Descripcion: %s \n la fecha de vencimiento es: %s \n la medida de este producto es: %s \n",p->name,p->workload,p->descripcion,p->FechaVencimiento,p->Medidaaaa);
	}
}

// Modificar el inventario del producto
void ListModify(SP *L)
{
	int a;
	char nam[40];
	SP *p = L->next;
	if (p == NULL)
		printf("¡Los datos están vacíos y no se pueden modificar!");
	else
	{
		printf("Introduzca el nombre de su producto modificado:");
		scanf("%s",nam);
		while(strcmp(p->name, nam) != 0)
		{
			p = p->next;
			if (p == NULL)
			{
				printf("No se encontró información relevante \n");
				return;
			}
		}
		printf("Introduzca su inventario revisado:");
		scanf("%d",&p->workload);
		printf("Modificado correctamente");
	}
}

// Eliminar información del producto
void ListDelete(SP *L)
{
	char n[40];
	SP *p = L->next, *pre = L; // Defina el puntero p para apuntar al nodo principal, defina pre para apuntar al nodo principal y pre siempre apunte al nodo predecesor de p
	if (p == NULL)
		printf("¡Los datos están vacíos y no se pueden borrar!");
	else
	{
		printf("Ingrese el nombre del producto que desea eliminar:");
		scanf("%s", n);
		while (strcmp(p->name, n) != 0)
		{
			pre = p;
			p = pre->next;
			if (p == NULL)
			{
				printf("No se encontró información relevante y no se puede eliminar \n");
				return;
			}
		}
		pre->next = p->next;
		free(p);
		printf("eliminado correctamente");
	}
}

// Insertar información relevante sobre el inventario de productos
void ListInsert(SP *L)
{
	SP *s = NULL; // Genera un nuevo nodo s
	s = (SP *)malloc(sizeof(SP));
	printf("Introduzca el número de producto del producto:");
	scanf("%s", s->no);
	printf("Introduzca el nombre del producto:");
	scanf("%s", s->name);
	printf("Por favor ingrese el inventario del producto:");
	scanf("%d", &s->workload);
	s->next = L->next;
	L->next = s;
	printf("¡Insertar correctamente!");
}

// Estadísticas del inventario total de bienes
void SumSp(SP *L)
{
	int sum=0;
	SP *p=L->next;
	while(p!=NULL)
	{
		sum+=p->workload;
		p=p->next;
	}
	printf("El inventario total del producto es%d \n",sum);    
}

// Clasifica el inventario de cada categoría
void Sort(SP *L)
{
	SP *p,*q,*tail,*l;
	tail=NULL;
	while((L->next->next) != tail)
	{
		p = L;
		q = L->next;
		while(q->next != tail)
		{
			if((q->workload) > (q->next->workload))
			{
				p->next = q->next;
				q->next = q->next->next;
				p->next->next = q;
				q = p->next;
			}
			q = q->next;
			p = p->next;
		}
		tail = q;
	}
	printf("El resultado del inventario de productos de pequeño a grande es el siguiente: \n");
	l=L->next;
	while(l!=NULL)
	{
		if(l->next!=NULL)
		{
			printf("%s(%d)->",l->name,l->workload);
			l=l->next;
		}
		else
		{
			printf("%s(%d)",l->name,l->workload);
			l=l->next;
		}
	}
}
// Ingrese información relevante sobre el inventario de productos
void Input(SP *p, int i)
{
	printf("Introduzca el número de producto del% d producto: ", i + 1);
	scanf("%s", p->no);
	printf("Introduzca el nombre del% d producto:", i + 1);
	scanf("%s", p->name);
	printf("Introduzca la fecha de vencimiento del% d producto: ", i + 1);
	scanf("%s", p->FechaVencimiento);
	printf("Introduzca el la medida que ocupa elmedicamento ya sea ml o gr del% d producto: ", i + 1);
	scanf("%s", p->Medidaaaa);
	printf("Introduzca la cantidad de inventario del% d producto: ", i + 1);
	scanf("%d", &p->workload);
	printf("Introduzca la descripcion del% d producto: ", i + 1);
	scanf("%[^.]", p->descripcion);
}

// Menú del sistema de gestión de inventario de productos básicos
void Menu()
{
	printf("\n\n");
	printf("\t\t\t =================== Sistema de gestión de inventario de productos básicos ==================== == \n ");
	printf("\t\t\t * Autor: XXX clase: XXXXXXXXXXX número de estudiante: XXXXXXXXXX * \n");
	printf("\t\t\t*                                                       *\n");
	printf("\t\t\t * 1>. Ingrese la información del inventario del producto * \n");
	printf("\t\t\t * 2>. Encuentra el inventario de un producto * \n");
	printf("\t\t\t * 3>. Modificar el inventario de un producto * \n");
	printf("\t\t\t * 4>. Eliminar información relacionada con el inventario de un determinado producto * \n");
	printf("\t\t\t * 5>. Insertar información sobre un producto determinado * \n");
	printf("\t\t\t * 6>. Cuente el inventario total de bienes * \n");
	printf("\t\t\t * 7>. Clasifique el inventario de cada categoría * \n");
	printf("\t\t\t * 0>. Salir del sistema de gestión * \n");
	printf("\t\t\t * ¡Bienvenido a usar este sistema! * \n");
	printf("\t\t\t========================================================\n");
	printf("\t\t\t tEntre las opciones, presione Entrar para ingresar las opciones: \n");
}
