# Codigos
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

#define NUM 5

struct FABRICA {
		char CODIGO[20] ;
		char MAQ ;
		int PUNTAJE[3];
		} ;

void CARGAR ( struct FABRICA [],int);                           //ACORDATE QUE ARRANCA EN INT.
void MIRAR ( struct FABRICA [],int);
float PROMEDIO(struct FABRICA);

void ORDENAR_POR_MAQUINA(struct FABRICA[],int);
void MIRAR_POR_MAQUINA(struct FABRICA[],int);

void MIRAR_POR_PIEZAS(struct FABRICA[],int);

int MAXIMO (struct FABRICA[],int);

int main()

{int I , j , POSMAX;
  struct FABRICA VEC[NUM];                                    //CODIGO SOBRE DE LA ESTRUCTURA EN EL MAIN OSEA (VEC), EN LA FUNCION LA PODES CAMBIAR A (V).

  CARGAR(VEC,NUM);                                 //SE LE PASA A TODO (MENOS A LA CARGA) NUM POR LA CONDICION DE FIN, ESTO ES PARA QUE NO HAYA ERROR.
  MIRAR(VEC,NUM);

  ORDENAR_POR_MAQUINA(VEC,NUM);
  MIRAR_POR_MAQUINA(VEC,NUM);

  MIRAR_POR_PIEZAS(VEC,NUM);

  POSMAX=MAXIMO(VEC,NUM);
  printf("\n EL NOMBRE %s DE LA MAQUINA %c :%.2f",VEC[POSMAX].CODIGO,VEC[POSMAX].MAQ,PROMEDIO(VEC[POSMAX]));
  printf("\n\n\n FIN DEL PROGRAMA\n\n");
}

void CARGAR ( struct FABRICA V[] , int N )                //LA CARGA DEVUELVE ALGO POR LA CONDICION DE FIN NO TE OLVIDES VA UN INT.
{   int I , J ;
    for ( I = 0 ; I < N ; I++ ) {            //algo importante esta es la condicion PARA QUE HAYA FIN, en caso de que no pida se resuelve normal fap osea (I=0; I < N; I++) Y TODO LO DEMAS. VUELAN EL FLAG Y EL NUM
    		printf("\n INGRESE CODIGO:");
    		fflush(stdin);
       		gets(V[I].CODIGO);
    		printf("\n INGRESE MAQ (A/B):");
       		scanf("%c",&V[I].MAQ);
       			for(J = 0; J < 3; J ++){
                    //V[I].PUNTAJE[J] =1+rand()%100;           //SI QUERES PROBAR EL PROGRAMA SACA EL RAND SINO DEJA EL RAND Y EN EL PARCIAL PONE EL MANUAL
                     INGRESO MANUAL DE PUNTAJES
                      printf("\n INGRESE PUNTAJE:");
                      scanf("%d",&V[I].PUNTAJE[J]);

       			}
    }

}

void MIRAR ( struct FABRICA V[] , int N)
{	int I,J;
	printf("\n\n MOSTRAR VECTOR\n");
	   printf("\n\n\n %-15s%12s%20s%30s\n" , "CODIGO" , "MAQ" , "PUNTAJES" , "PROMEDIOS" );
	for ( I = 0 ; I < N ; I++ ) {
		printf("\n\n %-15s%9c\t" , V[I].CODIGO , V[I].MAQ);
			for(J=0; J<3; J++)
				printf("%3d",V[I].PUNTAJE [J]) ;
				 printf ("\t\t  %.2f", PROMEDIO (V[I]));
    }
	getchar();
}

float PROMEDIO(struct FABRICA V)             //SOLO SE LE PASA LA ESTRUCTURA
{ int suma,I;
	  suma=0;
	for (I=0;I<3;I++)
	{
		suma+=V.PUNTAJE[I];
	}

	return (float)suma/3;
}

void ORDENAR_POR_MAQUINA(struct FABRICA V[] , int N)
{	int I, J;
	struct FABRICA AUX;
	for (I=0; I< N-1 ; I ++)
      for (J=0; J < N-I-1 ; J++)
		if ( ( V[J].MAQ > V[J + 1].MAQ ) || ( V[J].MAQ == V[J + 1].MAQ ) && (PROMEDIO (V[J]) < PROMEDIO (V[J+1])) ) //ordenamiento de menor a mayor (PARA LAS MUJERES EL PICO PARA >) (PARA LOS HOMBRES EL PICO PARA <) :D
		{
			AUX =  V [J] ;
			V [J] =  V [J+1];
			V [J+1] = AUX;
		}
	printf("\n ORDENADO POR MAQUINA");
	getchar();
}

void MIRAR_POR_MAQUINA(struct FABRICA V[],int N)
{int I,J;
    printf("\n\n\n %-15s%12s%20s\n" , "CODIGO" , "MAQUINA" , "PROMEDIOS" );
    for (I=0;I <N; I++){                                                    //VER LAS 5 MEJORES ALUMNAS ES UN EJEMPLO (EN CASO DE QUERER VER 10 CAMBIALE EL 5 POR EL 10) :D
        printf("\n\n %-15s%9c\t" , V[I].CODIGO , V[I].MAQ);
        printf ("\t %.2f", PROMEDIO (V[I]));
            }
    getchar();
}

void MIRAR_POR_PIEZAS(struct FABRICA V[],int N)
{int I,PD,SC,PC;
    PD=0;SC=0;PC=0;
    for (I=0;I <N; I++){
     if ((PROMEDIO (V[I])> 70 && PROMEDIO (V[I])< 100))
            PC++;
     if ((PROMEDIO (V[I])> 50) && (PROMEDIO (V[I])< 70) )
            SC++;
     if(PROMEDIO (V[I])< 50)
            PC++;
   }
   printf("\n\n\n CANTIDAD DE FIEZAS DE PRIMERA MANO: %d", PC);
   printf("\n\n\n CANTIDAD DE PIEZAS DE SEGUNDA MANO: %d", SC);
   printf("\n\n\n CANTIDAD PIEZAS DESCARTAS :%d", PD);
   getchar();
}

int MAXIMO(struct FABRICA V[],int N)
{ int max,posmax,I;

	max=PROMEDIO(V[0]);
	posmax=0;
		for (I=0; I<N; I++){
		   if (PROMEDIO(V[I]) > max)
			 {
				max=PROMEDIO(V[I]);
				posmax=I;
			 }
		}
	return posmax;
}

