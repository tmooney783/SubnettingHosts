<h1>In this project I learned how to subnet based on the amount of hosts needed in each subnet</h1>

I converted one network:

        10.1.1.0/24
       255.255.255.0

into 3 smaller subnetworks with 40 available hosts each.

First I converted the subnet mask to binary:

       255  .  255   .  255   .   0
    11111111.11111111.11111111.00000000

Then used the binary chart below (each number represents a bit in the host section) to determine how many host bits I need to save.
Starting from the right, it takes me 6 jumps to get to 64 (the first number large enough to provide me with 40 hosts),


    256 128 64 32  6  8  4  2
             ^  ^  ^  ^  ^  ^
             6  5  4  3  2  1


which means I have to save the last 6 bits from the host section of the subnet mask. 

**This is the only difference from subnetting based on amount of networks needed.**

My new subnet mask is:
 
       255  .  255   .  255   .   192
    11111111.11111111.11111111.11000000


New CIDR notation (all the 1's in the binary mask): /26

Increment (the last 1 in the network segment converted back to decimal): 64


    11111111.11111111.11111111.  1  1  0  0  0  0  0  0
                               128 64 32 16  8  4  2  1
                                    ^

Network ranges: 

    10.1.1.0   - 10.1.1.63
    10.1.1.64  - 10.1.1.127
    10.1.1.128 - 10.1.1.191

There are 64 hosts available in each network. 
To find this, I used 2^6-2.

**^6 because of the 6 remaining 0's in the host section of the binary mask.**
**-2 because 0 is always reserved for the network address and 255 is always reserved for the broadcast address.**

I then logically seperated the network into 3 smaller subnetworks by assigning hosts ip addresses from the 3 ranges.
