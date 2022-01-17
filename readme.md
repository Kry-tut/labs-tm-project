#Projekt Technika Mikroprocesorowa - Krystian Tutlewski
Co to za projekt
#Opis działania
opis
#Części wykorzystane w projekcie
części
#Schemat oraz części w Eagle
![img](./hardware/jeden.jpg)
![img](./hardware/dwa.jpg)
#Kod programu:
```cpp
#include <avr/io.h>
#include <util/delay.h>
#include <stdlib.h>
#include <avr/HD44780.h>
#include "avr/HD44780.c"

//definicje nazw dla LEDow
#define Led1 (1<<PA6)
#define Led2 (1<<PA7)
#define Led3 (1<<PC7)
#define Led4 (1<<PC6)
#define Led5 (1<<PC5)
#define Led6 (1<<PC4)
#define Led7 (1<<PC3)
#define Led8 (1<<PC2)
//definicje nazw dla Przyciskow
#define Enter (1<<PC1)
#define bit0 (1<<PC0)
#define bit1 (1<<PD7)
#define bit2 (1<<PD6)
#define bit3 (1<<PD5)
#define bit4 (1<<PD4)
#define bit5 (1<<PD3)
#define bit6 (1<<PD2)
#define bit7 (1<<PD1)
#define Clear (1<<PD0)

int main(void){

	//inicjowanie Wyjsc
	DDRA |= Led1;
	DDRA |= Led2;
	DDRC |= Led3;
	DDRC |= Led4;
	DDRC |= Led5;
	DDRC |= Led6;
	DDRC |= Led7;
	DDRC |= Led8;
	//inicjowanie Wejsc
	PORTC |= Enter;
	PORTC |= bit0;
	PORTD |= bit1;
	PORTD |= bit2;
	PORTD |= bit3;
	PORTD |= bit4;
	PORTD |= bit5;
	PORTD |= bit6;
	PORTD |= bit7;
	PORTD |= Clear;

	LCD_Clear();
	LCD_GoTo(0,0);
	LCD_WriteText("8bit kalkulator");
	LCD_GoTo(0,1);

	int liczba=0; //liczba koncowa
	int jeden=0, dwa=1, trzy=0, cztery=0, piec=0, szesc=0, siedem=0, osiem=0;
	char liczbaCHAR[3];
	while(1){

		if(!(PINC & bit0)){
			if(jeden==0){
				jeden=1;
				PORTA |= Led1;
			}
			else{
				jeden=0;
				if(PINA & Led1){
					PORTA ^= Led1;
				}
			}
		}
		if(!(PIND & bit1)){
			if(dwa==0){
				dwa=1;
				PORTA |= dwa;
			}
			else{
				dwa=0;
				if(PINA & Led2){
					PORTA ^= Led2;
				}
			}
		}
		if(!(PIND & bit2)){
			if(trzy==0){
				trzy=1;
				PORTC |= Led3;
			}
			else{
				trzy=0;
				if(PINC & Led3){
					PORTC ^= Led3;
				}
			}
		}
		if(!(PIND & bit3)){
			if(cztery==0){
				cztery=1;
				PORTC |= Led4;
			}
			else{
				cztery=0;
				if(PINC & Led4){
					PORTC ^= Led4;
				}
			}
		}
		if(!(PIND & bit4)){
			if(piec==0){
				piec=1;
				PORTC |= Led5;
			}
			else{
				piec=0;
				if(PINC & Led5){
					PORTC ^= Led5;
				}
			}
		}
		if(!(PIND & bit5)){
			if(szesc==0){
				szesc=1;
				PORTC |= Led6;
			}
			else{
				szesc=0;
				if(PINC & Led6){
					PORTC ^= Led6;
				}
			}
		}
		if(!(PIND & bit6)){
			if(siedem==0){
				siedem=1;
				PORTC |= Led7;
			}
			else{
				siedem=0;
				if(PINC & Led7){
					PORTC ^= Led7;
				}
			}
		}
		if(!(PIND & bit7)){
			if(osiem==0){
				osiem=1;
				PORTC |= Led8;
			}
			else{
				osiem=0;
				if(PINC & Led8){
					PORTC ^= Led8;
				}
			}
		}
		if(!(PINC & Enter)){
			LCD_GoTo(6,1);
			itoa(liczba, liczbaCHAR, 10);
			LCD_WriteText(liczbaCHAR);
		}
		if(!(PIND & Clear)){
			LCD_Clear();
			LCD_GoTo(0,0);
			LCD_WriteText("8bit kalkulator");
			LCD_GoTo(0,1);
			jeden=0;
			dwa=0;
			trzy=0;
			cztery=0;
			piec=0;
			szesc=0;
			siedem=0;
			osiem=0;
			liczba=0;
			if(PINA & Led1){
				PORTA ^= Led1;
			}
			if(PINA & Led2){
				PORTA ^= Led2;
			}
			if(PINC & Led3){
				PORTC ^= Led3;
			}
			if(PINC & Led4){
				PORTC ^= Led4;
			}
			if(PINC & Led5){
				PORTC ^= Led5;
			}
			if(PINC & Led6){
				PORTC ^= Led6;
			}
			if(PINC & Led7){
				PORTC ^= Led7;
			}
			if(PINC & Led8){
				PORTC ^= Led8;
			}
			itoa(liczba, liczbaCHAR, 10);
		}

		liczba=(jeden*1)+(dwa*1)+(trzy*1)+(cztery*1)+(piec*1)+(szesc*1)+(siedem*1)+(osiem*1);
		_delay_ms(300);


	}
}
```
