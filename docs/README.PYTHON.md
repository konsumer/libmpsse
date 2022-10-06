# Python: module mpsse

[index](.)  
[/usr/lib/python2.6/dist-packages/mpsse.py](file:/usr/lib/python2.6/dist-packages/mpsse.py)  
[Module Docs](http://docs.python.org/library/mpsse)

  
## Modules





[pylibmpsse](pylibmpsse.html)  

  
## Classes





[MPSSE](mpsse.html#MPSSE)

  
### class **MPSSE



Pythonclasswrapperforlibmpsse.



Methods defined here:  

### \_\_init\_\_(self, mode\=None, frequency\=100000, endianess\=0)

Classconstructor.  
  
@mode-The[MPSSE](#MPSSE)modetouse,oneof:SPI0,SPI1,SPI2,SPI3,I2C,GPIO,BITBANG,None.  
IfNone,noattemptwillbemadetoconnecttotheFTDIchip.UsethisifyouwanttocalltheOpenmethodmanually.  
@frequency-Thefrequencytouseforthespecifiedserialprotocol,inhertz(default:100KHz).  
@endianess-Theendianessofdatatransfers,oneof:MSB,LSB(default:MSB).  
  
ReturnsNone.

### Open(self, vid, pid, mode, frequency\=100000, endianess\=0, interface\=1, description\=None, serial\=None, index\=0)

OpensthespecifiedFTDIdevice.  
Calledinternallyby\_\_init\_\_ifthe\_\_init\_\_modeisnotNone.  
  
@vid-FTDIUSBvendorID.  
@pid-FTDIUSBproductID.  
@mode-The[MPSSE](#MPSSE)modetouse,oneof:SPI0,SPI1,SPI2,SPI3,I2C,GPIO,BITBANG.  
@frequency-Thefrequencytouseforthespecifiedserialprotocol,inhertz(default:100KHz).  
@endianess-Theendianessofdatatransfers,oneof:MSB,LSB(default:MSB).  
@interface-TheinterfacetouseontheFTDIchip,oneof:IFACE\_A,IFACE\_B,IFACE\_C,IFACE\_D,IFACE\_ANY(default:IFACE\_A).  
@description-FTDIdeviceproductdescription(default:None).  
@serial-FTDIdeviceserialnumber(default:None).  
@index-Numberofmatchingdevicetoopeniftherearemorethanone,startswithzero(default:0).  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexeptiononfailure.

### Close(self)

ClosestheFTDIdeviceconnection,deinitializeslibftdi,andfreesthelibmpssecontext.  
  
ReturnsNone.

### EnableBitmode(self, tf)

Enables/disablesbitwisedatatransfers.  
CalledinternallybyReadBitsandWriteBites.  
  
@tf-Setto1toenablebitwisetransfers,0todisable.  
  
ReturnsNone.

### ErrorString(self)

Returnsthelastlibftdierrorstring.

### FlushAfterRead(self, tf)

Enables/disablestheexplicitflushingoftherecievebufferaftereachreadoperation.  
  
@tf-Setto1toenableflushing,0todisable(disabledbydefault).  
  
ReturnsNone.

### GetAck(self)

ReturnsthelastreceivedACKbit.  
  
Returnsoneof:ACK,NACK.

### GetClock(self)

Returnsthecurrentlyconfiguredclockrate,inhertz.

### GetDescription(self)

ReturnsthedescriptionoftheFTDIchip,ifany.  
Thiswillonlybepopulatedif\_\_init\_\_wasusedtoopenthedevice.

### GetPid(self)

ReturnstheproductIDoftheFTDIchip.

### GetVid(self)

ReturnsthevendorIDoftheFTDIchip.

### PinHigh(self, pin)

SetsthespecifiedGPIOpinhigh.  
  
@pin-Pinnumber0-11inGPIOmode.  
Inallothermodes,oneof:GPIOL0,GPIOL1,GPIOL2,GPIOL3,GPIOH0,GPIOH1,GPIOH2,GPIOH3,GPIOH4,GPIOH5,GPIOH6,GPIOH7.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### PinLow(self, pin)

SetsthespecifiedGPIOpinlow.  
  
@pin-Pinnumber0-11inGPIOmode.  
Inallothermodes,oneof:GPIOL0,GPIOL1,GPIOL2,GPIOL3,GPIOH0,GPIOH1,GPIOH2,GPIOH3,GPIOH4,GPIOH5,GPIOH6,GPIOH7.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### PinState(self, pin, state\=-1)

Checksthecurrentstateofthepins.  
ForuseinBITBANGmodeonly.  
  
@pin-Thepinnumberwhosestateyouwanttocheck.  
@state-ThevaluereturnedbyReadPins.Ifnotspecified,ReadPinswillbecalledautomatically.  
  
Returnsa1ifthepinishigh,0ifthepinislow.

### Read(self, size)

Readsbytesovertheselectedserialprotocol.  
  
@size-Numberofbytestoread.  
  
Returnsastringofsizebytes.

### ReadBits(self, n)

Performsabitwisereadofupto8bitsatatime.  
  
@n-Numberofbitstoread.  
  
Returnsanintegervaluewiththereadbitsset.

### ReadPins(self)

Readsthecurrentstateofthechip'spins.  
ForuseinBITBANGmodeonly.  
  
Returnsanintegerwiththecorrespondingpin'sbitsset.

### SendAcks(self)

CausesallsubsequentI2Creadoperationstorespondwithanacknowledgement.  
  
ReturnsNone.

### SendNacks(self)

CausesallsubsequentI2Creadoperationstorespondwithano-acknowledgement.  
  
ReturnsNone.

### SetAck(self, ack)

SetsthetransmittedACKbit.  
ForuseonlyinI2Cmode.  
  
@ack-Oneof:ACK,NACK.  
  
ReturnsNone.

### SetCSIdle(self, idle)

Setstheidlestateofthechipselectpin.  
  
@idle-Setto1toidlehigh,0toidlelow(CSidleshighbydefault).  
  
ReturnsNone.

### SetClock(self, frequency)

Setstheappropriatedivisorforthedesiredclockfrequency.  
Calledinternallyby\_\_init\_\_andOpen.  
  
@frequency-Thedesiredclockfrequency,inhertz.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### SetDirection(self, direction)

Setstheinput/outputdirectionofpinsasdeterminedbydirection(1=Output,0=Input).  
ForuseinBITBANGmodeonly.  
  
@direction-Byteindicatinginput/outputdirectionofeachbit(1isoutput,0isinput).  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### SetLoopback(self, enable)

Enable/disableinternalloopback.Loopbackisdisabledbydefault.  
  
@enable-Setto1toenableloopback,0todisable(disabledbydefault).  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### SetMode(self, mode, endianess)

Setstheappropriatetransmitandreceivecommandsbasedontherequestedmodeandbyteorder.  
Calledinternallyby\_\_init\_\_andOpen.  
  
@mode-The[MPSSE](#MPSSE)modetouse,oneof:SPI0,SPI1,SPI2,SPI3,I2C,GPIO,BITBANG.  
@endianess-Theendianessofdatatransfers,oneof:MSB,LSB.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### Start(self)

Senddatastartcondition.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### Stop(self)

Senddatastopcondition.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### Transfer(self, data)

Transfersdataovertheselectedserialprotocol.  
ForuseonlyinSPI0,SPI1,SPI2,SPI3modes.  
  
@data-Astringofbytestobewritten.  
  
Returnsastringoflen(data)bytes.

### Tristate(self)

PutsallI/Opinsintoatristatemode(FT232Honly).

### Version(self)

Returnsthelibmpsseversionnumber.  
Highnibbleismajor,lownibbleisminor.

### Write(self, data)

Writesbytesoutviatheselectedserialprotocol.  
  
@data-Astringofbytestobewritten.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### WriteBits(self, bits, n)

Performsabitwisewriteofupto8bitsatatime.  
  
@bits-Anintegerofbitstobewritten.  
@n-Transmitnnumberofleast-significantbits.  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

### WritePins(self, data)

Writesanewstatetothechip'spins.  
ForuseinBITBANGmodeonly.  
  
@data-Anintegerwiththebitssettothedesiredpinstates(1=output,0=input).  
  
ReturnsMPSSE\_OKonsuccess.  
Raisesanexceptiononfailure.

  
### Data


```
ACK = 0  
BITBANG = 7  
FIFTEEN_MHZ = 15000000  
FIVE_MHZ = 5000000  
FOUR_HUNDRED_KHZ = 400000  
GPIO = 6  
GPIOH0 = 4  
GPIOH1 = 5  
GPIOH2 = 6  
GPIOH3 = 7  
GPIOH4 = 8  
GPIOH5 = 9  
GPIOH6 = 10  
GPIOH7 = 11  
GPIOL0 = 0  
GPIOL1 = 1  
GPIOL2 = 2  
GPIOL3 = 3  
I2C = 5  
IFACE_A = 1  
IFACE_ANY = 0  
IFACE_B = 2  
IFACE_C = 3  
IFACE_D = 4  
LSB = 8  
MPSSE_FAIL = -1  
MPSSE_OK = 0  
MSB = 0  
NACK = 1  
ONE_HUNDRED_KHZ = 100000  
ONE_MHZ = 1000000  
SIX_MHZ = 6000000  
SPI0 = 1  
SPI1 = 2  
SPI2 = 3  
SPI3 = 4  
TEN_MHZ = 10000000  
THIRTY_MHZ = 30000000  
TWELVE_MHZ = 12000000  
TWO_MHZ = 2000000
```