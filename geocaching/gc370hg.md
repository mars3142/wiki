---
title: GC370HG - Panzerknacker
layout: default
---
Das sollte mein erster Arduino-Cache (Codename) "Panzerknacker" werden.

## Sourcecode

{% hightlight c %}

/*--------------------------------------------------------------------------------------
 Includes
 --------------------------------------------------------------------------------------*/
#include <LiquidCrystal.h>   // include LCD library

/*--------------------------------------------------------------------------------------
 Defines
 --------------------------------------------------------------------------------------*/
#define EMPTYLINE      "                "
#define COPYRIGHTLINE1 "(c) 2012 by     "
#define COPYRIGHTLINE2 "mars3142        "
#define ACCESSGRANTED  "ACCESS GRANTED  "
#define ACCESSDENIED   "ACCESS DENIED   "
#define COORDINATEN    "N XX XX.XXX     " // real next north coordinates
#define COORDINATEE    "EXXX XX.XXX     " // real next east coordinates
#define CODEINPUT      "INPUT CODE      "

#define CODE           "0000"             // code to receive the next coordinates
#define NUMKEYS        5

/*--------------------------------------------------------------------------------------
 Init the LCD library with the LCD pins to be used
 --------------------------------------------------------------------------------------*/
LiquidCrystal lcd( 8, 9, 4, 5, 6, 7 );

/*--------------------------------------------------------------------------------------
 Initial code to display
 --------------------------------------------------------------------------------------*/
char* code;

/*--------------------------------------------------------------------------------------
 Position of the input cursor (zero based)
 --------------------------------------------------------------------------------------*/
int pos = 0;

/*--------------------------------------------------------------------------------------
 If solution is correct
 --------------------------------------------------------------------------------------*/
bool correct = false;

/*--------------------------------------------------------------------------------------
 loop of correct answer
 --------------------------------------------------------------------------------------*/
int loopCount = 0;

/*--------------------------------------------------------------------------------------
 Input value of keys
 (left, up, down, righ, select)
 --------------------------------------------------------------------------------------*/
int key_val[NUMKEYS] ={ 
  50, 200, 400, 600, 800 }; 

int old_key = -1;

/*--------------------------------------------------------------------------------------
 setup()
 Called by the Arduino framework once, before the main loop begins
 --------------------------------------------------------------------------------------*/
void setup()
{
  // set up the LCD number of columns and rows
  lcd.begin( 16, 2 );

  code = "0000";

  // print copyright
  printText( COPYRIGHTLINE1, COPYRIGHTLINE2 );
  delay( 1000 );

  clearDisplay();
}

/*--------------------------------------------------------------------------------------
 loop()
 Arduino main loop
 --------------------------------------------------------------------------------------*/
void loop()
{
  // read input
  int key = analogRead(0);
  key = get_key( key );

  if ( key != old_key ) 
  {
    switch ( key )
    {
    case 0: // right
      pos++;
      if (pos > 3) pos = 0;
      break;

    case 1: // up
      changeNumber( pos, +1 );
      break;

    case 2: // down
      changeNumber( pos, -1 );
      break;

    case 3: // left
      pos--;
      if (pos < 0) pos = 3;
      break;

    case 4: // select
      if (code == CODE)
      {
        correct = true;
      }
      else
      {
        showAccess(false);
        delay( 1000 );
      }
      break;

    default:
      key = -1;
    }
  }

  // show values
  if (!correct)
  {
    printText( CODEINPUT, code, 200 );
    printText( CODEINPUT, hideChar( code, pos ), 100 );
  }
  else
  {
    if ( loopCount == 0 ) showAccess( true );
    showCoordinates();
    loopCount++;
  }

  old_key = key;
}

/*--------------------------------------------------------------------------------------
 clearDisplay()
 Reset LCD display and wait 500ms
 --------------------------------------------------------------------------------------*/
void clearDisplay()
{
  lcd.clear();
  delay( 500 );
}

/*--------------------------------------------------------------------------------------
 showAccess()
 Show if access is granted or denied
 --------------------------------------------------------------------------------------*/
void showAccess(bool granted)
{
  if (!granted)
  {
    printText( ACCESSDENIED, EMPTYLINE, 1000 );
  } 
  else
  {
    printText( ACCESSGRANTED, EMPTYLINE, 1000 );
  }
}

/*--------------------------------------------------------------------------------------
 showCoordinates()
 Shows final coordinates
 --------------------------------------------------------------------------------------*/
void showCoordinates()
{
  clearDisplay();

  lcd.setCursor( 0, 0 );
  for ( int i = 0; i <= 14; i++ )
  {
    lcd.print( COORDINATEN[i] );
    delay(500);
  }

  lcd.setCursor( 0, 1 );
  for ( int i = 0; i <= 14; i++ )
  {
    lcd.print( COORDINATEE[i] );
    delay(500);
  }

  delay(2000);
}

/*--------------------------------------------------------------------------------------
 printText( char*, char* )
 prints text on LCD
 --------------------------------------------------------------------------------------*/
void printText( char* line1, char* line2 )
{
  printText( line1, line2, 0 );
}

/*--------------------------------------------------------------------------------------
 printText( char*, char*, int )
 prints text on LCD
 --------------------------------------------------------------------------------------*/
void printText( char* line1, char* line2, int delayTime )
{
  printText( line1, line2, delayTime, false );
}

/*--------------------------------------------------------------------------------------
 printText( char*, char*, bool )
 prints text on LCD
 --------------------------------------------------------------------------------------*/
void printText( char* line1, char* line2, bool center )
{
  printText( line1, line2, false );
}

/*--------------------------------------------------------------------------------------
 printText( char*, char*, int )
 prints text on LCD and waits a delay time
 --------------------------------------------------------------------------------------*/
void printText( char* line1, char* line2, int delayTime, bool center )
{
  lcd.setCursor( 0, 0 );
  lcd.print( line1 );
  lcd.setCursor( 0, 1 );
  lcd.print( line2 );

  delay( delayTime );
}

/*--------------------------------------------------------------------------------------
 char* hideChar( char*, int )
 disables the char at given position
 --------------------------------------------------------------------------------------*/
char* hideChar( char* text, int pos )
{
  char retValue [16];
  for ( int i = 0; i < 16; i++ )
  {
    if (i == pos)
    {
      retValue[i] = '_';
    }
    else
    {
      retValue[i]  = text[i];
    }      
  }
  return retValue;
}

/*---------------------------------------------------------------------------------------
 get_key( unsigned int )
 Convert ADC value to key number
 ---------------------------------------------------------------------------------------*/
int get_key(unsigned int input)
{
  int retValue;

  for (retValue = 0; retValue < NUMKEYS; retValue++)
  {
    if (input < key_val[retValue])
    {
      return retValue;
    }
  }

  if (retValue >= NUMKEYS) retValue = -1;  // No valid key pressed
  return retValue;
}

/*---------------------------------------------------------------------------------------
 changeNumber( int, int )
 increment or decrement the value at given position 
 ---------------------------------------------------------------------------------------*/
void changeNumber( int pos, int value )
{
  int val = atoi(&code[pos]);
  val += value;
  if (val < 0) val = 9;
  if (val > 9) val = 0;
  code[pos] = (char) val + '0';
}
{% endhighlight %}

## Stückliste

## Schaltplan