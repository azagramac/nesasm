## How to build

#### Linux
* Just run `make all` from `sources` directory
* Install run `make install` from `sources` directory

#### MacOS
* Install *argp-standalone* package using command: `brew install argp-standalone`
* Run `make all` from `sources` directory

#### Windows
* Install [MSYS2](https://www.msys2.org/)
* Install *base-devel*, *gcc*, *git* and *libargp-devel* packages using command: `pacman -S base-devel gcc git libargp-devel`
* Run `make all` from `sources` directory


## Usage

    Usage: nesasm [OPTION...] <source.asm>

      -C, --sequ=<name>=<value>  Assign a string value to a symbol
      -D, --equ=<name>=<value>   Assign an integer value to a symbol
      -f, --symbols[=<prefix>]   Create FCEUX symbol files
      -F, --symbols-offset=<offset>   Bank offset for FCEUX symbol files
      -i, --listing              Force listing
      -l, --listing-level=#      Listing file output level (0-3)
      -L, --listing-file=<file.lst>   Name of the listing file
      -m, --macro-expansion      Force macro expansion in listing
      -o, --output=<file.nes>    Name of the output file, use '-' for stdout
      -r, --raw                  Prevent adding a ROM header
      -s, --segment-usage        Show (more) segment usage
      -W, --warnings             Show overflow warnings
      -?, --help                 give this help list
          --usage                give a short usage message
      -V, --version              print program version



    Option             Description
    ------             -----------

     -o <file.nes>     Set output filename.
                       The default is input filename + ".nes" extension.
                       Use '-' for stdout output.

     -D <name>=<value> Assign an integer value to a symbol.
                       Example: -D delay=10
                       It will be equal to: delay .equ 10
                       at the beginning of your code, also you can use '$' and '%'
                       prefixes for hexadecimal and binary values.

     -C <name>=<value> Assign a string value to a symbol.
                       Example: -C image_file=image.bin
                       It will be equal to: image_file .sequ "image.bin"
                       at the beginning of your code.

     -f [prefix]       Enable generation of symbol files for FCEUX debugger,
                       optionally you can specify filenames prefix.

     -F [offset]       Set bank offset for FCEUX symbol files.

     -L <file.lst>     Set listing filename.
                       The default is output filename + ".lst" extension.

     -l #              Control output of the listing file:

                           0 - disable completely the listing file even if the
                               LIST directive is used in the input file
                           1 - minimun level; code produced by DB, DW and DEFCHR
                               will not be dumped
                           2 - normal level; only code produced by DEFCHR will not
                               be dumped
                           3 - maximun level; all the code is dumped in the
                               listing file

                       The default level is level 2.
                       
     -s                Show segment usage. If one of those options is specified
                       the assembler will display information on the ROM bank
                       usage. Use '-s' to show basic information and '-ss' to
                       show more detailed information.

     -i                Force listing file writing, even if the
                       LIST directive is not seen in the input file.

     -m                Force macros expansion in the listing file, even if the
                       MLIST directive is not seen in the input file.

     -r                Control the header generation. By default the assembler
                       always adds an header to the ROM file; unless '-raw' is
                       specified, in this case no ROM header is generated.

     -W                Show warnings on bank overflow when using .inc* directives.

### Instructions set
    ----------------
        +------+----------+-----------------------------+
        |      | NVTBDIZC | Description                 |
        +------+----------+-----------------------------+
        | ADC  | XX0---XX | Add with Carry              |
        | AND  | X-0---X- | Logical AND                 |
        | ASL  | X-0---XX | Arithmetic Shift left       |
        | BCC  | --0----- | Branch if Carry Clear       |
        | BCS  | --0----- | Branch if Carry Set         |
        | BEQ  | --0----- | Branch if Equal             |
        | BIT  | XX0---X- | Bit Test                    |
        | BMI  | --0----- | Branch if Minus             |
        | BNE  | --0----- | Branch if Not Equal         |
        | BPL  | --0----- | Branch if Plus              |
        | BRA  | --0----- | Branch Always               |
        | BRK  | --0----- | Break                       |
        | BVC  | --0----- | Branch if Overflow Clear    |
        | BVS  | --0----- | Branch if Overflow Set      |
        | CLC  | --0----0 | Clear Carry flag            |
        | CLD  | --0-0--- | Clear Decimal flag          |
        | CLI  | --0--0-- | Clear Interrupt disable     |
        | CLV  | -00----- | Clear Overflow flag         |
        | CMP  | X-0---XX | Compare A with source       |
        | CPX  | X-0---XX | Compare X with source       |
        | CPY  | X-0---XX | Compare Y with source       |
        | DEC  | X-0---X- | Decrement                   |
        | DEX  | X-0---X- | Decrement X                 |
        | DEY  | X-0---X- | Decrement Y                 |
        | EOR  | X-0---X- | Logical Exclusive OR        |
        | INC  | X-0---X- | Increment                   |
        | INX  | X-0---X- | Increment X                 |
        | INY  | X-0---X- | Increment Y                 |
        | JMP  | --0----- | Jump                        |
        | JSR  | --0----- | Jump to Sub Routine         |
        | LDA  | X-0---X- | Load A                      |
        | LDX  | X-0---X- | Load X                      |
        | LDY  | X-0---X- | Load Y                      |
        | LSR  | 0-0---XX | Logical Shift Right         |
        | NOP  | --0----- | No Operation                |
        | ORA  | X-0---X- | Logical inclusive OR        |
        | PHA  | --0----- | Push A                      |
        | PHP  | --0----- | Push P                      |
        | PLA  | X-0---X- | Pull A                      |
        | PLP  | XXXXXXXX | Pull P                      |
        | ROL  | X-0---XX | Rotate Left                 |
        | ROR  | X-0---XX | Rotate Right                |
        | RTI  | XXXXXXXX | Return from Interrupt       |
        | RTS  | --0----- | Return from Sub Routine     |
        | SBC  | XX0---XX | Substract with Carry        |
        | SEC  | --0----1 | Set Carry flag              |
        | SED  | --0-1--- | Set Decimal flag            |
        | SEI  | --0--1-- | Set Interrupt disable       |
        | STA  | --0----- | Store A                     |
        | STX  | --0----- | Store X                     |
        | STY  | --0----- | Store Y                     |
        | TAX  | X-0---X- | Transfer A to X             |
        | TAY  | X-0---X- | Transfer A to Y             |
        | TSX  | X-0---X- | Transfer S to X             |
        | TXA  | X-0---X- | Transfer X to A             |
        | TXS  | --0----- | Transfer X to S             |
        | TYA  | X-0---X- | Transfer Y to A             |
        +------+----------+-----------------------------+

    Operand syntax
    --------------
        A        accumulator
        #i       immediate
        <n       zero page
        <n,X     zero page indexed by X
        <n,Y     zero page indexed by Y
        [n]      indirect (*)
        [n,X]    indirect pre-indexed by X (*)
        [n],Y    indirect zero page post-indexed by Y
        r        relative
        n        absolute
        n,X      absolute indexed by X
        n,Y      absolute indexed by Y

        (*) can be zero page or absolute


### Expressions

The assembler supports very complex expressions. You can use as many level of parenthesis as you want and spaces between operators and numbers are possible.
        
Numbers can be written in three bases : hexadecimal ($7F),  binary (%0101) and decimal (48). Character values are also supported ('A').

All the usual operators are present :

    +, -, *, /, %, ^, &, |, ~, <<, >>

As well as the comparison operators :

    =, !=, !, <, >, <=, >=

For the priority, the same rules as C apply.

You can also use predefined or user-defined functions in an expression.


### Predefined functions

* HIGH()   - Returns the high byte of a value.
* LOW()    - Returns the low byte.
* BANK()   - Returns the bank index of a symbol. If no symbol, or more than one, are given, the function will return an error.
* PAGE()   - Returns the page index of a label. See above for errors.
* SIZEOF() - Returns the size of a data element.


### Predefined constants

There are predefines NES register addresses:

* PPUCTRL and PPU_CTRL     - $2000
* PPUMASK and PPU_MASK     - $2001
* PPUSTATUS and PPU_STATUS - $2002
* OAMADDR and OAM_ADDR     - $2003
* OAMDATA and OAM_DATA     - $2004
* PPUSCROLL and PPU_SCROLL - $2005
* PPUADDR and PPU_ADDR     - $2006
* PPUDATA and PPU_DATA     - $2007
* OAMDMA and OAM_DMA       - $4014
* SQ1VOL and SQ1_VOL       - $4000
* SQ1SWEEP and SQ1_SWEEP   - $4001
* SQ1LO and SQ1_LO         - $4002
* SQ1HI and SQ1_HI         - $4003
* SQ2VOL and SQ2_VOL       - $4004
* SQ2SWEEP and SQ2_SWEEP   - $4005
* SQ2LO and SQ2_LO         - $4006
* SQ2HI and SQ2_HI         - $4007
* TRILINEAR and TRI_LINEAR - $4008
* TRILO and TRI_LO         - $400A
* TRIHI and TRI_HI         - $400B
* NOISEVOL and NOISE_VOL   - $400C
* NOISELO and NOISE_LO     - $400E
* NOISEHI and NOISE_HI     - $400F
* DMCFREQ and DMC_FREQ     - $4010
* DMCRAW and DMC_RAW       - $4011
* DMCSTART and DMC_START   - $4012
* DMCLEN and DMC_LEN       - $4013
* APUSTATUS and APU_STATUS - $4015
* JOY1                     - $4016
* JOY2 and JOY2_FRAME      - $4017


### User-defined functions

User-defined functions are declared with the .FUNC directive, for example:

    SCR_ADDR .func (\1) + ((\2) << 5)

Up to nine arguments, \1 to \9, can be used.
                                                    
To call a function simply enclose arguments within parenthesis and separate them with a comma:

    stw #SCR_ADDR(10,4)+$2000,<$20

User-defined functions can be very useful, one often needs to use the same calculation again and again in expressions. Defining a function will save you a lot of work, and reduce typo errors. :) Note that function calls can be nested, you can call one function from another without any problem, however, recursive calls will produce an error.


### Macros

While functions are very useful to replace common expressions by just a function call, macros are used to replace common groups of instructions by a single line of code. 

You start a macro definition with:

    label  .macro

Or you can also place the label after the '.macro' keyword, like this:

    .macro label 

After follow the body of the macro, which is terminated by the '.endm' directive.

As an example let's define a 'neg' macro to negate the accumulator.

    neg    .macro
            eor   #$FF
            inc   A
           .endm

Macros can also have parameters. In the macro body, you refer to a parameter by using the backslash character ('\') followed by a digit. Nine parameters can be used, \1 to \9.

Here's another example:

    add    .macro       ; add a value to register A
            clc         ; (handle carry flag)
            adc   \1+1
           .endm

Other 'special' parameters can be used, here's a list of all the possible parameter you can use inside a macro:

    Parameter  Description
    ---------  -----------
    \1  -  \9  Input parameter - up to nine can be used in a macro call

    \#         Number of input parameters

    \?1 - \?9  Returns 'type' of input parameter:
                 ARG_NONE      (= 0) = No argument
                 ARG_REG       (= 1) = register            -> A, X, Y
                 ARG_IMMEDIATE (= 2) = Immediate data type -> #xx
                 ARG_ABSOLUTE  (= 3) = Abosulte addressing -> label, $xxxx
                 ARG_INDIRECT  (= 4) = Indirect addressing -> [label]
                 ARG_STRING    (= 5) = String argument     -> "..."
                 ARG_LABEL     (= 6) = Label argument      -> label

    \@         Special parameter that returns a different number for
               each macro; can be used to define local symbols inside
               macros:

                    abs    .macro
                           lda   \1
                           bpl   .x\@
                           eor   #$FF
                           inc   A
                           sta   \1
                   .x\@:
                          .endm

### Directives

    LIST    - Enable the listing file generation. You can later stop
              temporarily the output with the NOLIST directive and
              restart it again with LIST.

    NOLIST  - Stop the listing output.

    MLIST   - Allow macro expansion in the listing file.

    NOMLIST - Stop expanding macros in the listing file. This directive
              won't have any effect if you use the '-m' command line
              option.

    EQU     - Assign an integer value to a symbol. The character '=' has
              the same function too.

    SEQU    - Assign a string value to a symbol.

    BANK    - Select a 8KB ROM bank (0-127) and reset the location
              counter to the latest known position in this bank.

    ORG     - Set the location of the program counter. The thirteen
              lower bits of the address inform the assembler about
              the offset in the ROM bank and the third upper bits
              represent the page index.

    DB      - Store one or more data bytes at the current location.
    
    STR     - Stores a string, the first byte is the length of the string, 
              followed by the string content, 
              The effect is equivalent to . DB is preceded with a length, 
              here's a small example:
                  ;use DB specified a length + string:
                  DB 12,"Hello World!"
                  ;can be replaced with STR:
                  STR "Hello World!"
    
    DW      - Store data words.

    BYTE    - Same as DB.

    WORD    - Same as DW.

    DS      - Reserve space at the current location. This space will
              be filled with zeroes if this directive is used in the
              CODE or DATA group.

    RSSET   - Set the internal counter of the RS directive to 
              a specified value.

    RS      - Assign a value to a symbol; a bit like EQU but here
              the value assigned is taken from an internal counter,
              and after the assignation this counter is increased
              by the amount specified in the RS directive.
              This is a very handy way of defining structure member
              offsets, here's a small example:

                  ; C:
                  ; --
                  ; struct {
                  ;    short p_x;
                  ;    short p_y;
                  ;    byte p_color;
                  ; } pixel;
                  ;
                  ; ASM:
                  ; ----

                          .rsset $0  ; set the initial value of RS counter
                  P_X     .rs 2
                  P_Y     .rs 2
                  P_COLOR .rs 1

              You can later use these symbols as offsets in a 'pixel'
              struct:

                  ldy #P_COLOR
                  lda [pixel_ptr],Y

    MACRO   - Start a macro definition.

    ENDM    - End a macro definition.

    INCBIN  - Include a binary file at the current location. If the file
              is bigger than a ROM bank, as many successive banks as
              necessary will be used.

    INCLUDE - Include a source file at the current location.
              Up to 7 levels are possible.
    DEFCHR  - Define a character tile (8x8 pixels). The directive takes
              8 arguments (stored as 32-bit values of 8 nybbles each),
              one argument for each row of pixel data. This directive
              takes also care to reorganize the pixel data to the NES
              required bit format. Note that only color indexes 0 to 3
              can be used, as the NES tiles are only 4-color. An error
              will be generated if you try to use more colors.

                  zero:   .defchr  $00111110,\
                                   $01000011,\
                                   $01000101,\
                                   $01001001,\
                                   $01010001,\
                                   $01100001,\
                                   $00111110,\
                                   $00000000

    ZP      - Select the Zero-Page section ($0000-$00FF).

    BSS     - Select the RAM section ($0200-$07FF).

    CODE    - Select the program code section.

    DATA    - Select the program data section.

              Note: In ZP and BSS sections you can only allocate storage,
              ----  you can *not* store initial values.

    IF      - Conditional assembly directive. This directive will evaluate
              the supplied expression and then turn conditional assembly
              on or off depending on the result. If the result is null
              conditional assembly is turned off, and on if the result is
              non null.
    IFDEF
    IFNDEF  - These directives allow conditional assembly depending on
              whether a label is defined or not.

    ELSE    - Toggle conditional assembly on to off, or vice verca.

    ENDIF   - Terminate the current level of conditional assembly.
              Report an error if the number of IF's and ENDIF's doesn't
              match.

    FAIL    - When the assembler encounters this directive, it aborts
              the compilation. Can be used within a macro for argument
              error detection.

    INESPRG - Specifies the number of 16k PRG banks or just PRG size if it > $EFF.

    INESCHR - Specifies the number of 8k CHR banks or just CHR size if it > $EFF.

    INESMAP - Specifies the NES mapper used, up to 4095.

    INESSUBMAP - Specifies the NES submapper used, up to 15.

    INESMIR - Specifies VRAM mirroring of the banks.
              0: Horizontal or mapper-controlled, 1: Vertical, 2: Hard-wired four-screen

    INESPRGRAM - Specifies the size of PRG RAM.

    INESPRGNVRAM - Specifies the size of PRG NVRAM (non-volatile).

    INESCHRRAM - Specifies the size of CHR RAM.

    INESCHRNVRAM - Specifies the size of CHR NVRAM (non-volatile).

    INESBAT - Specifies "battery" and other non-volatile memory
              0: Not present, 1: Present

    INESTIM - Specifies CPU/PPU timing
              0: RP2C02 ("NTSC NES"), 1: RP2C07 ("Licensed PAL NES"), 2: Multiple-region, 3: UMC 6527P ("Dendy")
