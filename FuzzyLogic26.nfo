;
; >> 26 bytes Fuzzy Logic <<<
;
; 2012-11-02 by JAC!
;
; Based on https://pouet.net/prod.php?which=60648
;
; Hey, this is my first C64 prod.
; I had expected it to be different, but I think
; TV noise is always a good starting point when
; discovering a new platform.
;
; Have fun understanding this one :-)
;
; @com.wudsn.ide.lng.hardware=C64

        opt h-

op_shx  = $9e                 ;SHX abs,y
op_ror  = $6e                 ;ROR abs
op_sta  = $85                 ;STA zp
ptr     = op_ror-1            ;Operand re-use

        org $32c-1            ;IN: <A>=0, <X>=0, <Y>=$0a, <C>=1
        .word $32d
        .byte $03             ;Change only high byte in $32e: $ff2f to $032f

loop    .byte op_sta, ptr+1
        .byte a($d1d8)        ;<C>=1, so $15/$8b, use mirror so opcode is CMP izy
        nop                   ;Cannot believe myself I put a NOP in a 32 bytes demo
        sta $d400,y           ;Hi SID, how are you
        .byte op_shx,a($d3e0) ;SHX $d3e0,y, store 0 to mirrors of $d020/$d021
        adc $d012             ;Hmm, VIC looks a bit random today
        sta (ptr),y
        iny
        and #$0f              ;Increased memory range
        ora #$20
        bne loop
