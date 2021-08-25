This repo has configurations for getting the MKS_GEN_L v1/v2 boards to work with the LCD_For_Melzi v4 from the Wanhao Duplicator i3 and other printers

This is the printer:

https://www.wanhao3dprinter.com/Unboxin/ShowArticle.asp?ArticleID=70

This is the board: 

https://reprap.org/wiki/MKS_GEN

And this is the LCD:

https://ultimate3dprintingstore.com/collections/duplicator-i3-parts/products/wanhao-duplicator-3-series-lcd-display



This is the LCD Pinout:

https://imgur.com/a/g3MIFPU

This is the MKS board pinout:

https://wiki.openastrotech.com/power-wiring/screenshot_2020-12-09_193750.png



This is the writeup of the problem so far:

https://www.reddit.com/r/3Dprinting/comments/ojqy3s/trying_to_get_a_wanhao_i3_display_to_work_with_a/

https://www.reddit.com/r/3Dprinting/comments/p9i0md/i_dont_know_if_i_setup_marlin_properly/



One thing I was told to try was:

https://www.reddit.com/r/3Dprinting/comments/95hgd6/connecting_the_monoprice_maker_select_v21_lcd_to/



Currently ive figured out that i should be able to configure the marlin firmware for the LCD pins to something like this, instead of having to rewire the LCD, which looks pretty trick, due to hpw the wiring harness works:

#define LCD_PINS_RS 17
#define LCD_PINS_ENABLE 16
#define LCD_PINS_D4 11
#define BTN_ENC 28
#define BTN_EN1 29
#define BTN_EN2 30

I slid this bit of programming in a #ifndef LCD_FOR_MELZI...#endif in the pins_MKS_Gen_L.h file, this does not seem to work, because...

...when looking at marlin and the Conditionals_LCD.h file, i see that therein is:

#if ENABLED(REPRAP_DISCOUNT_FULL_GRAPHIC_SMART_CONTROLLER) || ENABLED(LCD_FOR_MELZI) || ENABLED(SILVER_GATE_GLCD_CONTROLLER)
  #define DOGLCD
  #define U8GLIB_ST7920
  #define REPRAP_DISCOUNT_SMART_CONTROLLER
#endif

so i also have tried changing the #ifndef LCD_FOR_MELZI to a #ifndef REPRAP_DISCOUNT_SMART_CONTROLLER in the pins_MKS_Gen_L.h file, but this also yeilds nothing.

one thing i have to note is that i did have to grind off a orientation tab on the connector cable for the LCD, to get it to fit properly as the connector is suppossed to be plugged in 180o to how its wired....






