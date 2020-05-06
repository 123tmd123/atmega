# atmega

#include <mega128.h>
#include <delay.h>

char forward[4] = {0x09, 0x05, 0x06, 0x0a};
char rewind[4] = {0x0a, 0x06, 0x05, 0x09};
char fnd[3] = {0x06, 0x5b, 0x4f}; 
char *data;
char motor_mode;
/**/
//int led[8] = {0x7f, 0xbf, 0xdf ,0xef, 0xf7, 0xfb, 0xfd ,0xfe}; 

int led[3] = {0x7f, 0xbf, 0xdf }; 

    
/**/
void main(void)
{
    char n, i;
    DDRA = 0xff;
    DDRC = 0xff;
    PORTC = 0xff;
    motor_mode = 0;
  //  data = forward;  
    
    /*****/
                   
      /* 
      while(1)  
  {
    for(i=0; i<8; i++)
    {
     PORTC = led[i];
     delay_ms(300);
    }
    
    for(i=7; i>-1; i--)
    {
     PORTC = led[i];
     delay_ms(300);
    } 
  }
  */
     
     
    /****/
                         
    DDRB = 0xff;     		// 포트 B 출력 설정
    DDRF = 0b11110000;		// PF4-PF7 출력 설정
    
    while(1)
    {
       data = forward;
       for(n=0;n<36;n++) // 6 > 180
       {
         for(i=0;i<4;i++)
         {
            PORTA = *(data + i);
            delay_ms(15);  
                              
            
         } 
          
         	 PORTF = 0b11100000;
             PORTB = fnd[n/12];   
             PORTC = led[n/12];
             /**/
                
                 
             /**/
       }  
                                
           
              PORTC = 0xff;
               delay_ms(300);

    data = rewind;   
   
         for(n=0;n<36;n++) // 6 > 180
       {
         for(i=0;i<4;i++)
         {
            PORTA = *(data + i);
            delay_ms(15);
         }
         
         PORTF = 0b11100000;    
                      
         
       if(n<=12){  
         PORTB = fnd[2]; 
         PORTC = led[2];
        }else if(n>13 && n<24)
        {
         PORTB = fnd[1]; 
         PORTC = led[1];
        }else if(n>24 && n<36)
        {
         PORTB = fnd[0]; 
         PORTC = led[0];
        }
       
       }   
                        
       
   //       delay_ms(20);
//     PORTC = PORTC ^ 0xff;
  //        delay_ms(20); 
  
   PORTC = 0xff;
    
    }   
    

    
}

/*
interrupt [EXT_INT4] void aa_int4(void)
{   
 

 motor_mode = motor_mode ^ 1;
 if(motor_mode == 0)
 {
 data= rewind;
 }else{
  data = forward;
  }
  
                                
}   
 */



/*      
char forward[4] = {0x09, 0x05, 0x06, 0x0a};
char rewind[4]  = {0x0a, 0x06, 0x05, 0x09};
char *data;

void main(void)
{
 unsigned char n , i = 0, key;
 DDRA = 0xff;
 DDRC = 0xff;
 DDRE = 0;
 while(1)
 {
  key = PINE & 0xf0;
  if(key == 0b11100000)
  {
   PORTC = 0xf0;
   data = forward;
   if(i>=4) i = 0;
   PORTA = *(data+i);
   delay_ms(500);
   i++;
  } 
       
  else if(key == 0b11010000)
  {
   PORTC = 0x0f;
   data = rewind;
   if(i>=4) i = 0;
   PORTA = *(data + i );
   delay_ms(500); 
    i++;
  }
 
 
 }

}
*/

 
 
/*   
unsigned char forward[4] = {0x01, 0x04, 0x02, 0x08};
unsigned char rewind[4] = {0x08, 0x02, 0x04, 0x01};
char motor_mode;
unsigned char *data;

void main(void){

unsigned char n, i;
DDRA = 0xff;
DDRC = 0Xff;
motor_mode = 0;
data = forward;

EICRB = 0b00000010;
EIMSK = 0b00010000;
SREG = 0x80;

while(1)
{
 for(n=0 ; n < 12 ; n++)
 {
  for( i = 0 ; i < 1 ; i++)
  {
     PORTA = *(data + i);
     delay_ms(100);
  } 
 }
 PORTC = PORTC ^ 0xff;
 delay_ms(1);
} 
   
}                               

//extern interrupt 4 service rutine
interrupt [EXT_INT4] void aa_int4(void)
{   
 

 motor_mode = motor_mode ^ 1;
 if(motor_mode == 0)
 {
 data= rewind;
 }else{
  data = forward;
  }
  
                                
}

 */


  
                 
/*
char forward[4]= {0x01, 0x04, 0x02, 0x08}; // PA0, PA1, PA2, PA3
char *rewind;

void main(void)
{
  unsigned char n, i;
  rewind = forward;  
  DDRA = 0xff;                
  DDRC = 0xff;
  
  n = 0;
  
  while(n<12)
  {
  for(n=0 ; n<12 ; n++){   // 7.6 * 12 * 4 = 360 
    for(i = 0 ; i < 4 ; i++)  //7.5 * 24 & 4 = 720
    {
        PORTA  = *(rewind + i ); // i = 0 -> 7.5, i = 1 -> 15
        delay_ms(50);
    }   
  }
  PORTC = PORTC ^ 0xff; // led appear
  delay_ms(50);   
     
  
  
  
  } 


} 

*/

/*
#include <stdio.h>
#include <lcd.h>
#asm
        .equ __lcd_port = 0x12; //PORTD
#endasm

#define OCT4_DO 1912
#define OCT4_RE	1702
#define OCT4_MI 1516
#define OCT4_PA	1432
#define OCT4_SO	1278
#define OCT4_RA	1136
#define OCT4_SI	1004

#define OCT5_DO 956
#define OCT5_RE	851
#define OCT5_MI 758
#define OCT5_PA	716
#define OCT5_SO	639
#define OCT5_RA	568

#define OCT5_SI	 507
#define OCT6_DO	 477
 
int tone_table[60] = { //어머님 은혜 56개
	 OCT5_DO, OCT5_SI, OCT5_RA, OCT5_SO,
     OCT5_PA, OCT5_MI, OCT5_RE, OCT5_DO,
     OCT5_SO, OCT5_RA, OCT5_RA, OCT5_SI, OCT5_SI, OCT5_DO,
 
	 OCT5_DO, OCT5_DO, OCT5_SI, OCT5_RA,
     OCT5_SO, OCT5_SO, OCT5_MI, OCT5_DO,
     OCT5_DO, OCT5_SI, OCT5_RA, OCT5_SO, OCT5_SO, OCT5_MI, 
	
	OCT5_RE, OCT5_RE, OCT5_SO, OCT5_PA,
	OCT5_MI, OCT5_RE, OCT5_DO, OCT5_RE,
	OCT5_MI, OCT5_MI, OCT5_PA, OCT5_SO, OCT5_RA, OCT5_SO,
 
	OCT6_DO, OCT6_DO, OCT5_SI, OCT5_RA,
	OCT5_SO, OCT5_RA, OCT5_SO, OCT5_MI,
	OCT5_RA, OCT5_RA, OCT5_SO, OCT5_RA, OCT5_SI, OCT6_DO
	};

unsigned char *sound_table[] = {
 "OCT5_DO", "OCT5_SI", "OCT5_RA", "OCT6_SO",
 "OCT6_PA", "OCT5_MI", "OCT5_RE", "OCT5_DO",
 "OCT5_SO", "OCT5_RA", "OCT5_RA", "OCT5_SI", "OCT5_SI", "OCT5_DO",
 
 "OCT5_DO", "OCT5_DO", "OCT5_SI", "OCT6_RA",
 "OCT6_SO", "OCT5_SO", "OCT5_MI", "OCT5_DO",
 "OCT5_DO", "OCT5_SI", "OCT5_RA", "OCT5_SO", "OCT5_SO", "OCT5_MI",
 "OCT5_RE", "OCT5_RE", "OCT5_SO", "OCT5_PA",
 "OCT5_MI", "OCT5_RE", "OCT5_DO", "OCT5_RE",
 "OCT5_MI", "OCT5_MI", "OCT5_PA", "OCT5_SO", "OCT5_RA", "OCT5_SO",
 
 "OCT6_DO", "OCT6_DO", "OCT5_SI", "OCT5_RA",
 "OCT5_SO", "OCT5_RA", "OCT5_SO", "OCT5_MI",
 "OCT5_RA", "OCT5_RA", "OCT5_SO", "OCT5_RA", "OCT5_SI", "OCT6_DO"                                
                                     
                              };
                              
                              /*
도시라솔파미레도

솔라라시시도

도도시라솔솔미

도도시라솔솔미

미미미미파솔

파미레레레미파

미레도도라솔파미파 미레도



출처: https://inog.tistory.com/174 [이노그 이야기]
                              */
 /*
unsigned char *sound_table[] = {  
 "OCT5_MI", "OCT5_PA", "OCT5_SO", "OCT6_DO",
 "OCT6_DO", "OCT5_SI", "OCT5_RA", "OCT5_SO",
 "OCT5_RA", "OCT5_SO", "OCT5_SO", "OCT5_PA", "OCT5_MI", "OCT5_RE",
 
 "OCT5_MI", "OCT5_PA", "OCT5_SO", "OCT6_DO",
 "OCT6_DO", "OCT5_SI", "OCT5_RA", "OCT5_SO",
 "OCT5_RA", "OCT5_SO", "OCT5_PA", "OCT5_MI", "OCT5_RE", "OCT5_DO",
 "OCT5_RE", "OCT5_RE", "OCT5_SO", "OCT5_PA",
 "OCT5_MI", "OCT5_RE", "OCT5_DO", "OCT5_RE",
 "OCT5_MI", "OCT5_MI", "OCT5_PA", "OCT5_SO", "OCT5_RA", "OCT5_SO",
 
 "OCT6_DO", "OCT6_DO", "OCT5_SI", "OCT5_RA",
 "OCT5_SO", "OCT5_RA", "OCT5_SO", "OCT5_MI",
 "OCT5_RA", "OCT5_RA", "OCT5_SO", "OCT5_RA", "OCT5_SI", "OCT6_DO"};
   

int time_table[60] = {
		32, 16, 16, 32,
		48, 32, 16, 16,
		32, 16, 16, 16, 16, 96,
 
		32, 16, 32, 16,
		16, 16, 16, 48,
		32, 16, 16, 16, 16, 96,

		32, 16, 32, 16,
		16, 16, 16, 48,
		32, 16, 16, 16, 16, 96,

		32, 16, 32, 16,
		16, 16, 16, 48,
		32, 16, 16, 16, 16, 96};

    int tone_data, time_data;  	  // 주파수, 음길이 변수
    void Timer_interrupt_setup(void);  // 타이머/카운터0 초기설정
    void Auto_mode(void);

    void main(void){
     	 DDRE = 0x08;   // PORTE.3 방향설정
       DDRC = 0XFF;
       lcd_init(16);
       lcd_clear();

      Timer_interrupt_setup();
       while(1){
       Auto_mode();
       PORTC = 0;
       delay_ms(400);
       PORTC = 0xff;
       delay_ms(400);
       }
      }

    void Auto_mode(void){
      int  i, buf = 0;
      char lcd_text[16];
      for(i = 0; i < 56; i++)
          {
            tone_data = tone_table[i];  // i=0 이면 758
		       time_data = time_table[i]; // i=0 이면 32
		       sprintf(lcd_text, "  %s  ", sound_table[i]); // i=0 OCT5_MI
            lcd_gotoxy(0,1);
            lcd_puts(lcd_text);

		       while(time_data)
		          {
			           DDRE = 0x80;    // int7 출력
                       PORTE = 0x08;   // speak 출력 1
			           buf = tone_data;  // i=0 이면 32
			           while(buf--);      // 32,31,30....0

			           PORTE = 0x00;   // speak 출력 0
			           buf = tone_data;  // i=0 이면 32
			           while(buf--);     // 32,31,30....0
			         }
       }
 }
 // 타이머/카운터0 초기값 설정
 void Timer_interrupt_setup(void)
  {
    ASSR = 0;
    TCCR0 = 7;  // normal mode, 1024분주
    TCNT0 = 0;
    TIMSK = 1;  // TOIE0 = 1
    #asm("sei")   // SREG = 0x80 같음
  }
 interrupt [TIM0_OVF] void music(void)
  {
   time_data--;
  }

*/ 

/*                     
void main(void) {
 unsigned char i; 
 unsigned char k;
 DDRE =0x08; //PE.3 output direction setting
 TCCR3A = 0x43; // 0000 0100 0100 0011
 TCCR3B = 0x19; // 0001 1001 0001 1001
 TCNT3H = 0; 
 TCNT3L = 0;
 OCR3AH = 0;
 OCR3AL = 0;
 
 while(1)
 {
   if(PINE.4==0)
   {
     TCCR3A = 0x40; //COM3A1, A0 = 01 compare match OC3A TOGGLE
     for( i = 0 ; i < 3; i++)
     {
      //256Hz = 16MHz / [ 2*N(1+OCR3)] // N = 1 bunju
      // OCR3 = 31249 = 0x7A11
      OCR3AH = 7999 >> 8;  //OCR3AH = 7A
      OCR3AL = 7999 & 0X00ff;
      delay_ms(300);
           
     }
   }
 
 } 
 


}
*/





/*
void main(void) {
 unsigned char i;
 unsigned char k;
 
 DDRE = 0x08; //PE.3 output
 // timercounter 3 init  to make  lkhz OCR3A = 7999
 // CTC Mode, TOP = OCR3A
 // OC3A output: Toggle
    
 
 TCCR3A = 0x40; //COM3A1, A0  = 01 compare math -> OC3A TOGGLE output
 TCCR3B = 0x09; // WGM33,32,31,30 = 0100(CTC), CS02,01,01 
 TCNT3H = 0;
 TCNT3L = 0;
 OCR3AH = 0;
 OCR3AL = 0;
 
 while(1)
 {
   // cylen sound select
   if(PINE.4 == 0){
        TCCR3A=0x40;//COM3A1,A0 = 01 in compare match OC3A TOGGLE output
        for(i=0 ; i<3; i++){
        //256Hz = 16MHz / [2*N(1+PCR3] // N = 1bun
        // to question OCR value - > OCR3 = 31249 = 0x7A11
        OCR3AH = 500 >> 8; // OCR3AH = 7A
        OCR3AL = 500 & 0x00ff; //OCRAL = 11
        TCCR3B = 0x09;
        delay_ms(300);
        //340Hz = 16MHz/[2*N(1+OCR3)]
        //OCR3 = 23528
        //OCR3AH = 23528 >> 8;
        OCR3AH = 500 >> 8; 
        //OCR3AL = 23528 & 0x00ff;
        OCR3AL = 500 & 0x00ff;
        delay_ms(300);
   }
 }
 
 
 // bell sound select
   
   if(PINE.5 == 0) 
   {
     for( k = 0 ; k < 5 ; k++)
       {
         TCCR3A = 0x40;
         for( i = 0 ; i < 10 ; i++)
           {
            //480Hz = 16MHz/2*N(1+OCR)
            //OCR1 = 16664
            //OCR3AH = 16664 >> 8;
            OCR3AH = 16664 >> 8;
            OCR3AL = 16664 & 0x00ff;
            // same TCNT1H = TCNT1L = 0;
            TCCR3B = 9;
            //320Hz = 16MHz/2*N(1*OCR3)
            
            //OCR1 = 24999 // (8M-320)/320
            OCR3AH = 23999 >> 8;
            OCR3AL = 24999 & 0x00FF;
            delay_ms(300);
           }             
           
           //OC3A output stop
           OCR3AH = 0;
           OCR3AL = 0;
           TCCR3A = 0;
           delay_ms(300);
           
         
       }
       }
        //OC3A output stop
        OCR3AH = 0;
        OCR3AL = 0;
        TCCR3A = 0;
        
   
   }
}                


*/

/*
unsigned int pwm = 0x0200;  // current output compare register value 
 
void main(void)
{
  DDRB = 0xff;         //OCIC(PB7) output setting
  EIMSK = 0b00110000;  // extern INT4 = 1, INT 5 = 1
  EICRB = 0b00001010;  // extern interrupt
  SREG = 0x80;
  TCCRIA = 0b000011011;
  TCCR1B = 0x05;
  TCCR1C = 0;
  TCNT1 = 0;
  OCR1CH = (pwm) >> 8; 
  OCRICL = pwm & 0x00ff;
}  

interrupt [EXT_INT4] void aa_int4(void){
 if(pwm > 0x0050) pwm -= 0x0040;   
 OCR1CH = (pwm) >> 8;
 OCR1CL = pwm;
}                        

interrupt [EXT_INT5] void bb_int5(void){
 if(pwm > 0x03B0) pwm += 0x0040;   
 OCR1CH = (pwm) >> 8;
 OCR1CL = pwm;
}             


*/

/*
char led = 0b11111110;
  



void main(void)
{
   //port init
   DDRC = 0xff;  //Port C output setting
   
   PORTC = led;  //Port C init output
   
   // interrup init
   SREG = 0x80;  // global interrupt enable bit 1 set
   ETIMSK  = 0x04;  //TOIE3 = 1
   TCCR3A = 0;
   TCCR3B = 0x06;   //T3 falling edge counting, 0x07 -> rising edge
   TCCR3C  = 0;
   TCNT3H = 0xff; 
   TCNT3L = 0xfe;
   
   
}




interrupt [TIM3_OVF] void aa_int3(void)
{
  
   led <<=1;
   led |= 1;
   if(led == 0xff) led = 0xff;
   PORTC = led;
   TCNT3H = 0xff;
   TCNT3L = 0xff;
}
  
*/

/*               

unsigned char led = 0xfe;
unsigned int time = 0xea60; // TCNT1 = 40000(10bi), 9C40(16 bi)
                            // TCNT1 = 60000(10bi), 9ea60(16 bi)      init value
             
void main(void)
{                
  DDRC  = 0xff;    //port C output  60000 ~ 65535
  PORTC = led;     // PORT C init   ]
  //interrupt init
  TIMSK = 0x10;    //TETEL = 1
  TCCR1A = 0;      // mode 0 (normal mode)
  TCCR1B = 0x0c;   // presCaler  256
  TCCR1C = 0;
  TCNT1 = time;   // T/C1 register init : 40000
  SREG = 0x80;    // global interrupt enable bit to 1 set
  while(1);
}          


interrupt [TIM1_OVF] void aa_int1(void)
{
  //led sequence on/off
   led <<=1;
   led |= 0x01;
   if(led == 0xff) led = 0xfe;
   PORTC = led;
   TCNT1 = time;
}


*/
  
  
  
/*  
  
char seg[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7c, 0x27, 0x7f, 0x67};
int n1 = 0;
int n10 = 0;
int num = 0;
int i = 0;
char led = 0xfe;

void main(void) 
{
 DDRC = 0xff;
 PORTC = led;
 DDRB = 0xff;
 DDRF = 0xff;
 
 TIMSK = 0x40;
 TCCR2 = 0x64;
 OCR2 = 100;
 TCNT2 = 0;
 SREG = 0x80;
 while(1);
 
}

//TCNT2 = OCR2 interrupt service rution
interrupt [TIM2_OVF] void aa_int2(void) {
 num++;
 n1 = num % 10;
 n10 = num / 10;
 for(i = 0 ; i < 49 ; i++){
  PORTF = 0xe0;
  PORTB = seg[n1];
  delay_ms(10);
  PORTF = 0xd0;
  PORTB = seg[n10];
  if(num>99) num = 0;
  delay_ms(10);
 }
  led = (led << 1) | 0x01; // or calculate
  if(led == 255) led = 254;
  PORTC = led;
}


*/



/*
unsigned char led = 0xfe;
unsigned cnt = 0;

void main(void)
{
  DDRC = 0xff;
  PORTC = led;  //0xfe inital output
  // interrupt init
  TIMSK = 0x40; // TOIE2 = 1
  TCCR2 = 0x04; // normal mode, 256 bunju
  TCNT2 = 0;
  SREG = 0x80;
  while(1); 
}


interrupt [TIM2_OVF] void aa_int2(void) 
{
 cnt++;
 if(cnt == 250)
 {
   led <<=1;
   led |= 1;
   
   if(led == 0xff) led = 0xfe;
     PORTC = led;
     cnt = 0;
 }

}
*/       

//timer 16Mhz hz dependency 
/*       
char seg[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7c, 0x27, 0x7f, 0x67};
int n1 = 0;
int n10 = 0;
int num = 0;
int i = 0;
char led = 0xfe;

void main(void)
{
  DDRC = 0xff;
  PORTC = led;
  DDRB = 0xff;
  DDRF = 0xff;
  TIMSK = 1; //TOIE0 = 1  /0100 0111
  TCCR0 = 0x47;   //pc pwm 1024 bunju, COM01,00 = 1.0
  OCR0 = 127; //OCR0 = 127 give duty rate - 50 : 50
  TCNT0 = 0;  // T/C0 resister init value
  #asm("sei") // # asm("sei") is the same ass SREG = 0x80
  while(1); // you can use as if you were using SREG = 0x80
             //this is, the same
}                               

//TCNT0 = OCR0 interrupt service rutine 
interrupt [TIM0_OVF] void as_int0(void)
{
  num++;
  n1 = num % 10;
  n10 = num/10;
  for(i = 0 ; i < 49 ; i++)
  {
   PORTF = 0xe0;
   PORTB = seg[n1];
   delay_ms(10);
   PORTF = 0xd0;
   PORTB = seg[n10];
   if(num > 99) num = 0;
   delay_ms(10);
  }
 led = (led << 1) | 0x01; // or cal
 if(led == 255) led = 254;
 PORTC  = led;
 
}
 
*/ 
  
  
  
  
  
/*  
unsigned char led = 0xfe;
void main(void)

{
 // port init
 DDRC = 0xff;  // port C OUTPUT setting
 PORTC = led;  // port C init output 
 DDRB = 0xff;  // port B output setting
                                       
 // interrupt setting 01101101
 TIMSK = 0x02;  // OCIE0 = 1
 TCCR0 = 0x6f; //1024, FAST PWM MODE, COM01, COM00  = 10 01101111
 OCR0 = 255;  // output appera register
 TCNT0 = 0; // timer / count0 register init
 SREG = 0x80;  // interrupt access bit 1 set
 while(1);
}


//TCNT0 = OCR interrupt service rutine
//interrupt effect period  1/16[us] * 1024 bunju * 256 = 16.384[ms]

interrupt [TIM0_COMP] void aa_comp0(void)
{
 //LED sequence on/off
 led<<=1;
 led|=0x01;
 if(led == 255) led = 254;
 PORTC = led;
}            


    
  
  
  
  */
  

/*

unsigned char led = 0xff;
int count;
     
void main(void)
{
 DDRC = 0xff;
 count = 0; // interrupt count
 DDRB = 0xff;                 
 DDRF = 0x00;
 PORTC = led;
 TIMSK = 0x01; // TOIE0 = 1
 TCCR0 = 0x06;   //256 bunju  mormal mode
 TCNT0 = 0x06;   // 256-6 = 250
 SREG = 0x80;  // interrupt access bit 7 set
 
 while(1);
 
 }
 
 // 1/16 [us] * 256 bunju * 250(=256-6) = 4[ms]
 
 // led on/off    T = 4[ms] X 250 = 1 [sec]
 // ex) led - on/off bunju  T = 4[ms] X 15000 = 60[sec] 1 bun
interrupt [TIM0_OVF] void aa_int0(void)
{
  count++; 
  TCNT0=6;
  
  if(count == 150) 
  {
    PORTF =0xcf; PORTB = 0x3f;
    DDRF = 0xff ^ DDRF;
    led = led ^ 0xff;  //led = 0xff ? oxff, 0x00 ? oxff
    PORTC = led;
    count = 0;   
  } 
  
}


*/

 



/* 
unsigned char led = 0xfe;   //CTC
void main(void)
{
   // port init
   DDRC = 0xff;
   PORTC = led;
   DDRB = 0xff;
   DDRF = 0xff;
   PORTF = 0;
   
   // interrupt init
   TIMSK = 0x02; // OCIE0 = 1
   TCCR0 = 0x0f; // CS2, CS1, CS0 = 1024, WGM01, WGM00 = CTC
   OCR0 = 255;
   
   // output register value
   TCNT0 = 0;     //T/C 0 register value
   SREG = 0x80;   // interrupt access
   
   while(1)
   {
     PORTB = 255;
     delay_ms(500);
     PORTB = 0;
     delay_ms(500); 
   }
   
}   
// T/C 0 output 

//interrupt  T = 1/16[us] * 1024 bunju *(255-0)

//  = 16.384[ms]

interrupt [TIM0_COMP] void aa_comp0(void)
{
 //LED 
 led <<=1;
 led |= 0x01;
 if(led == 0xff) led = 0xfe;
 PORTC = led;
}
  
   
*/   
    
    
                      
  
/*  
char seg[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7c, 0x27, 0x7f, 0x67};
int n1 = 0;
int n10 = 0;
int num = 0;
char led = 0xfe;  
int i = 0;

void main() {

  DDRF = 0xff;
  DDRB = 0xff;
  DDRC = 0xff;
  PORTC = led;     
  
  TIMSK  = 0x01;  // TOIE0 = 1  // overflow interrupt access
  TCCR0 = 0x01;  // normal mode, com = 0 decline, bunju rate
  TCNT0 = 0x00;  // interrupt rate maximum 
  SREG = 0x80;                    
  
}
 

      
interrupt [TIM0_OVF] void aa_int()
{           
   num++;
   n10 = num / 10;
   n1 = num % 10;
   for(i = 0; i < 100 ; i++)
   { 
   
    PORTF = 0xe0;
    PORTB = seg[n1];
    delay_ms(5);
    
    PORTF = 0xd0;
    PORTB = seg[n10];
    if(num > 99) num = 0;
    delay_ms(5);
   
   }

     led = (led << 1) | 0x01;
     if(led == 0xff) led = 0xfe;
     PORTC = led;


}
  */         


/*
int num = 0;
char seg_data[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f};
void interrupt_call(int);
void main()
{
 DDRB = 0xff;   //   <- -> out  
 DDRF = 0x10;   //   <- -> out
 TIMSK = 1;     //   TOIE0 = 1
 TCCR0 = 7;     //   normal mode, CS02 CS01 CS00 = 1024 bunju
 TCNT0 = 0;     //   inital 0
 SREG = 0x80;   //   interrupt access 
}
  
interrupt [TIM0_OVF] void aa_int0(void)
{
  interrupt_call(num);
  num++;
  if(num == 10) num =0;

}         

void interrupt_call(int num) {
int i;
for(i = 0 ; i<10 ; i++)
{
 PORTF = 0b11100000;
 PORTB = seg_data[num];
 delay_ms(100);
 PORTF = 0b11110000;
}

}

*/  
  
/*
unsigned char led = 0xfe;

void main(void)
{
  DDRC = 0xff;      
  PORTC = led;
  DDRB = 0xff;
  PORTF = 0;
  DDRF = 0xff;
  TCNT0 = 0;      //resister inital
  TIMSK = 0x01; //nomal mode   TOIE0 = 1
 // TOIE0 = 1;
  TCCR0 = 0x07;
  SREG = 0x80;
  
  while(1)
  {
    PORTB = TCNT0;
    delay_ms(100);
    PORTB = TCNT0;
    delay_ms(100); 
  }
}
                 
   
   
// interrupt add 1/16 us * 1024 bunju @256 =16.384[ms]

interrupt [TIM0_OVF] void aa_int0(void)
{
  //LED  
  led<<=1;
  led|=1;
  if(led == 0xff) led =0xfe;
  PORTC = led;
} 

 */                




/*
int i, j, k, l = 0;
char data[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x7f, 0x6f};

void main(void){
 DDRB = 0xff;
 DDRF = 0xf0;
 SREG = 0x80;
 EICRB = 0b10101010;
 EIMSK = 0b11110000;
 
 while(1)
 {
  PORTF = 0b11100000;
  PORTB = data[i];
  if(i>=10) i = 0, k++;
  delay_ms(5);
  
  
  PORTF = 0b11010000; 
  PORTB = data[k];
  if(k>=10) k=0;  k++;
  delay_ms(5);
  
  if(j>=10) j = 0, j++;
  delay_ms(5);
  PORTF = 0b10110000; 
  PORTB = data[j];
  
  if(l>=10) l = 0, l++;
  delay_ms(5);
  PORTF = 0b01110000; 
  PORTB = data[l];
}  
  
interrupt [EXT_INT4] void aa_4(void){
   i++;
}  

interrupt [EXT_INT5] void bb_5(void){
   j++;
}  
  
interrupt [EXT_INT6] void cc_6(void){
   k++;
}   
 
interrupt [EXT_INT7] void dd_7(void){
   l++;
} 
 
}


*/    
   
        
/**

char fnd_data[10] = { 0x3f, 0x06, 0x5b, 0x4f, 0x3f, 0x6d, 0x7d, 0x07, 0x7f };          
char fnd1 = 0, fnd10 = 0, fnd100 = 0, fnd1000 = 0;
void fnd4_out(void);  


void main(void){
  DDRB = 0xff; DDRF = 0xf0;
  SREG = 0x80; EIMSK = 0xf0;
  EICRB = 0xaa;
  while(1)
  fnd4_out(); 
}
    


void fnd4_out(void)
{

 PORTF = 0b11100000;
 PORTB = fnd_data[fnd1];
 delay_ms(1); 
 PORTF = 0b11010000;          
 PORTB = fnd_data[fnd10];
 delay_ms(1);
 PORTF = 0b10110000;
 PORTB = fnd_data[fnd100];
 delay_ms(1);
 PORTF = 0b01110000;
 PORTB = fnd_data[fnd1000];
 delay_ms(1);
 
  

}



interrupt [EXT_INT4] void aa_4(void) {
   fnd1 = (fnd1 + 1) % 10; 
}

interrupt [EXT_INT5] void bb_5(void) {
   fnd10 = (fnd10 + 1) % 10; 
}

interrupt [EXT_INT6] void cc_6(void) {
   fnd100 = (fnd100 + 1) % 10; 
}

interrupt [EXT_INT7] void dd_7(void) {
   fnd1000 = (fnd1000 + 1) % 10; 
}
  

**/


/*
void main(void)
{
 DDRB = 0xff;
 DDRF = 0b11110000;  
 DDRC = 0xff;
 
 //interrupt init
 EICRB = 0b00000010;
 EIMSK = 0b00010000;
 SREG = 0x80;
 
 PORTF = 0b11100000;   
 PORTC = 0x03;    
 
 
 
 while(1)
   PORTB = fnd_data[data];

}
            

interrupt [EXT_INT4] void int_4(void)
{
  if(data==5 ) 
  {
  data = 0; 
  PORTC =0xff; 
  bin = 0x03;
  }
  PORTC <<=2; 
  
  PORTC = PORTC | bin;
  
  PORTF = 0xf3;
  PORTF >>=2;
          
  data++;
}                  


 */



/*
  for(i=0 ; i<7; i++)
  {
  PORTC = led;          
  Delay(10);
  led >>=1;          //led = led << 1; 
  
                    //0x7f
  }
*/  

// B = Segment
// C = LED
// F = Segment place 



/*
char flag = 1;
char data[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f};      
//char data_m[2] = {0x00, 0x40}; // 0x40 '-' appaear
//int absnum = 0;           

void main (void) {
 char i = 1;
 DDRB = 0xff;
 DDRF = 0xf0;
 DDRC = 0xff;
 PORTF = 0b11000000;
 SREG = 0x80;
 EICRB = 0b00000010;
 EIMSK = 0b00010000;
 
 while(1)
 {
   if(flag == 1) 
   {
    PORTB = data[i];
    i++;
    delay_ms(300);
    if(i==10) i = 0; 
   }
   else if (flag == 0) {
     PORTC = 0;
     delay_ms(300);
     PORTC = 0xff;
     delay_ms(300);
   
   
   } 
 }
 
 
}

interrupt [EXT_INT4] aa_4(void) {
   flag = flag^1;
}

*/


/*

void main (void) {
int n1 = 0;
int n10  = 0;
int n100 = 0;
int n1000 = 0;
int buf = 0;

DDRB = 0xff;
DDRF = 0xff;
SREG = 0x80;
EICRB = 0b10101010;
EIMSK = 0b11110000;

while(1)
{               
  n1000 = num / 1000;
  buf = num % 1000;
  n100 = buf / 100;
  buf = buf % 100;
  n10 = buf / 10;
  n1 =  buf % 10;
  
  PORTF = 0b11100000;     PORTB = data[n1];  delay_ms(5);
  PORTF = 0b11010000;     PORTB = data[n10];  delay_ms(5);
  PORTF = 0b10110000;     PORTB = data[n100];  delay_ms(5);
  PORTF = 0b01110000;     PORTB = data[n1000];  delay_ms(5);
  
  if( num > 9999) num = 0;
  }
}

interrupt [EXT_INT4] aa_4(void) {
   num++;
}

interrupt [EXT_INT5] bb_5(void) {
   num++;
}

interrupt [EXT_INT6] cc_6(void) {
   num++;
}

interrupt [EXT_INT7] dd_7(void) {
   num++;
}





/*PORTB = 0x3f;


while(1) {
if(data ==0){
 PORTB = 0x06;
 PORTC = 0b11111100;
 PORTF = 0x7f;
} else if(data == 1)
{ 
  PORTC = 0b11110011;
  PORTB = 0x5b;
  PORTF = 0x7f;
} else if( data == 2) {
    PORTC = 0xcf;
    PORTB = 0x4f;
    PORTF = 0x7f;
} else if( data == 3) {
   PORTC = 0x3f;
   PORTB = 0x66;
   PORTF = 0x7f;
}               

 */
            

/*  
char data = 0;
void main(void) {

DDRC = 0xff;    

EICRB =  0b00000010;
EIMSK  = 0b00010000;
SREG = 0x80;
 
  
                       
while(1)
{
  if(data==1) PORTC = 0b11111100;
  else if(data == 2) PORTC = 0b11110011;
  else if(data == 3) PORTC = 0xef;
  else if(data == 4) PORTC = 0x3f;
} 
  
  PORTC = 0xf0;

}
  
interrupt [EXT_INT4] void aa_4(void)
{
  data = (data + 1) % 5; // 0~9 apper value
}

*/


/*
char fnd_data[10] = { 0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f };          
char data = 0;
void main(void)
{
 DDRB = 0xff;
 DDRF = 0b11110000;
 
 //interrupt init
 EICRB = 0b00000010;
 EIMSK = 0b00010000;
 SREG = 0x80;
 
 PORTF = 0b11100000;
         
 while(1)
   PORTB = fnd_data[data];

}


interrupt [EXT_INT4] void int_4(void)
{
  data = (data + 1) % 10; // 0~9 apper value
}

*/

/*
char flag = 1;
char data[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f};      
//char data_m[2] = {0x00, 0x40}; // 0x40 '-' appaear
//int absnum = 0;           

void main (void) {
 char i = 1;
 DDRB = 0xff;
 DDRF = 0xf0;
 DDRC = 0xff;
 PORTF = 0b11000000;
 SREG = 0x80;
 EICRB = 0b00000010;
 EIMSK = 0b00010000;
 
 while(1)
 {
   if(flag == 1) 
   {
    PORTB = data[i];
    i++;
    delay_ms(300);
    if(i==10) i = 0; 
   }
   else if (flag == 0) {
     PORTC = 0;
     delay_ms(300);
     PORTC = 0xff;
     delay_ms(300);
   
   
   } 
 }
 
 
}

interrupt [EXT_INT4] aa_4(void) {
   flag = flag^1;
}

*/


/*

void main (void) {
int n1 = 0;
int n10  = 0;
int n100 = 0;
int n1000 = 0;
int buf = 0;

DDRB = 0xff;
DDRF = 0xff;
SREG = 0x80;
EICRB = 0b10101010;
EIMSK = 0b11110000;

while(1)
{               
  n1000 = num / 1000;
  buf = num % 1000;
  n100 = buf / 100;
  buf = buf % 100;
  n10 = buf / 10;
  n1 =  buf % 10;
  
  PORTF = 0b11100000;     PORTB = data[n1];  delay_ms(5);
  PORTF = 0b11010000;     PORTB = data[n10];  delay_ms(5);
  PORTF = 0b10110000;     PORTB = data[n100];  delay_ms(5);
  PORTF = 0b01110000;     PORTB = data[n1000];  delay_ms(5);
  
  if( num > 9999) num = 0;
  }
}

interrupt [EXT_INT4] aa_4(void) {
   num++;
}

interrupt [EXT_INT5] bb_5(void) {
   num++;
}

interrupt [EXT_INT6] cc_6(void) {
   num++;
}

interrupt [EXT_INT7] dd_7(void) {
   num++;
}


*/




/*

char data[10] = {0x3f, 0x06, 0x5b, 0x4f, 0x66, 0x6d, 0x7d, 0x07, 0x7f, 0x6f};
int num =0;             




      
void main(void) {
  int n1, n10 = 0;
  DDRB = 0xff; 
  DDRF = 0xff;
  SREG = 0x80;
  EICRB = 0b00001010;
  EIMSK = 0b00110000;
  
  while(1)
 { 
   n10 = num / 10;
   n1 = num % 10;
   PORTF = 0b11100000;
   PORTB = data[n1];
   delay_ms(5);
   PORTF = 0b11010000;
   PORTB = data[n10];
   delay_ms(5);
   if(num > 99)  num = 0;
   if(num < 0 )  num = 0;

  }

}      
      



        
// interrupt source name
interrupt [EXT_INT4] int_4(void){
 num++;
}

interrupt [EXT_INT5] int_5(void){
 num--;
}

*/

/*****
char i;
char data[4] = {0x3f, 0x06, 0x5b, 0x4f, 0};

void main(void) {
 
DDRC = 0xff;  
DDRB = 0xff;
DDRF = 0xff;     

PORTF = 0b11100000;

SREG = 0x80;
EIMSK = 0b11110000;
EICRB = 0b10101010;
 
while(1)
{
  for(i=0; i<5; i++)
  {
  PORTC = 0;
  delay_ms(500);
  PORTC = 0xff;
  delay_ms(500);  
  /////
  PORTB = 0x3f;
  delay_ms(500);
  
  }
}        
}
   
interrupt [EXT_INT4] void aa_4(void)
{
   for(i = 0 ; i < 5 ; i++)
   {
     LED4 = 0;
     delay_ms(500);
     LED4 = 1;
     delay_ms(500);
     PORTB = data[0];
   } 
  
}    




interrupt [EXT_INT5] void bb_5(void)
{
   for(i = 0 ; i < 5 ; i++)
   {
     LED5 = 0;
     delay_ms(500);
     LED5 = 1;
     delay_ms(500);  
     PORTB = data[1];
   } 
}


interrupt [EXT_INT6] void cc_6(void)
{
   for(i = 0 ; i < 5 ; i++)
   {
     LED6 = 0;
     delay_ms(500);
     LED6 = 1;
     delay_ms(500);   
     PORTB = data[2];
   } 
}



interrupt [EXT_INT7] void dd_7(void)
{
   for(i = 0 ; i < 5 ; i++)
   {
     LED7 = 0;
     delay_ms(500);
     LED7 = 1;
     delay_ms(500); 
     PORTB = data[3];
   } 
}


****/





    










/*  
char data[4] = {0x3f, 0x06, 0x5b, 0x4f};
void main(void) 
{
  DDRB = 0xff;
  DDRF = 0xf0;
  PORTF = 0b11100000;
  PORTB = 0x3f;
  SREG = 0x80;
  EIMSK = 0b11110000;
  EICRB = 0b10101010;
  
  while(1); // inturrupt resting
}

// interrupt 

interrupt [EXT_INT4] void aa_4(void)
{
   PORTB = data[0];
}                  

interrupt [EXT_INT5] void bb_5(void)
{
   PORTB = data[1];
}                  


interrupt [EXT_INT6] void cc_6(void)
{
   PORTB = data[2];
}                  


interrupt [EXT_INT7] void dd_7(void)
{
   PORTB = data[3];
}                  


*/  
  
  
/*

void main(void)
{
 unsigned char 
 led = 0xfe;
 DDRC = 0xff; 
 DDRF = 0xff;
 DDRB = 0xff;
 PORTC = led;
 SREG = 0x80;
 EICRB = 0b00001000;      // falling edge
 EIMSK = 0b00100000;      // masking
 
 while(1){
   do{
      PORTB = 0;
      PORTC = led;
      delay_ms(400);
      led <<= 1;
      led |= 0x01;
     }
     while(led != 0x7f);
     
     do{ 
         PORTB = 0;
         PORTC = led;
         delay_ms(400);
         led >>= 1;
         led |= 0x80;
       }
       
     while(led != 0xfe);
     
   }
}

interrupt [EXT_INT4] void aa_int4(void)
{
   PORTB = 0x3f;
   delay_ms(3000);
}


*/
