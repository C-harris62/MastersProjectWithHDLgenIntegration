# Test Plan 

The test table can be captured in, e.g, Notepad++ editor, with no tab characters, and with a pre-defined format, expected bt the ChatGPT testbench stimulus generation prompt header.

Example RV32I RiSC-V Register Bank (RB) test table

Inputs               ce  RWr rd    WBDat    rs1   rs2
Outputs                                                 rs1D     rs2D
                     1'b 1'b 5'b   32'h     5'b   5'b   32'h     32'h
        TestNo delay                                                      Note
        1      1     1   1   00100 deadbeef 00100 00100 deadbeef deadbeef Write RB(4),        Read RB(4) on rs1D  and rs2D
        2      1     1   1   00101 c001cafe 00100 00101 deadbeef c001cafe Write RB(5),        Read RB(4) on rs1D  and RB(5) on rs2D)
        3      1     1   1   00110 f00dcafe 00110 00100 f00dcafe deadbeef Write RB(6),        Read RB(6) on rs1D  and RB(4) on rs2D
        4      0.1   1   1   00110 a5a5a5a5 00110 00110 f00dcafe f00dcafe No write until clk, Read RB(6) on rs1D  and rs2D
        5      0.9   1   1   00110 a5a5a5a5 00110 00101 a5a5a5a5 c001cafe Write RB(6) on clk, Read RB(6) on rs1D  and RB(5) on rs2D
        6      3     1   1   11111 3c3c3c3c 11111 00110 3c3c3c3c a5a5a5a5 Write RB(31),       Read RB(31) on rs1D and RB(6) on rs2D
        7      3     1   1   00000 5a5a5a5a 11111 00000 3c3c3c3c 00000000 Write RB(0),        Read RB(31) on rs1D and RB(0)=0 on rs2D (write 0x5a5a5a5a to x0 does not occur)
        8      1     0   1   00100 c001100c 00100 11111 deadbeef 3c3c3c3c Write/read RB(4),   with ce deasserted. Read RB(4) on rs1D and RB(31) on rs2D
        9      1     1   1   00100 c001100c 00100 00100 c001100c c001100c Write RB(4),        Read RB(4) on rs1D and rs2D
        10     1     1   0   00110 ffffffff 00110 00110 a5a5a5a5 a5a5a5a5 Write RB(6),        with RWr deasserted. Read RB(6)on rs1D and rs2D
        11     1     1   1   00001 ffffffff 00001 00001 ffffffff ffffffff Write RB(1),        Read RB(1)on rs1D and rs2D

Format (referenced in the testbench ChatGPT header)
	row 1: input signal names
	row 2: output signal names
	row 3: signal radix
	row 4: TestNo, delayValue and Note column headings
	column 2: TestNo value
	column 3: delayValue values, specified as integer or real numbers  