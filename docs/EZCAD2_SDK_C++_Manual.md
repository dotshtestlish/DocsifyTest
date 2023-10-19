<a name="Lagof"></a>
# Summarize
<br />MarkEzd.dll file is Dynamic Link Library provided by Beijing JCZ Technology CO. LTD for developing software based on ezcad2 and lmc board<br />MarkEzdDll.h is header file of the exports function in MarkEzd.dll<br />We can develop the software using VC6.0.<br />The calling way of MarkEzd.dll is explicitly link. Developer needs to load and free MarkEzd.dll by calling Windows API function.

The steps are as follows.

1.  Call Windows' API function LoadLibrary() to load DLL dynamically; 
2.  Call Windows' API function GetProcAddrress() to get the pointer of the functions in the DLL and use the function pointer to finish the work; 
3.  Call Windows’ API function FreeLibrary() to release library when you do not use DLL or the program ends. 

Note: the program that calls MarkEzd.dll must be located at the same folder with ezcad2.exe. Or else the program would not work. And ezcad2.exe and markEzd.dll cannot work as usually at the same time, so you must close ezcad2.exe when MarkEzd.dll is used.

<a name="TPCBk"></a>
# Description
<br />Return value of most functions in MarkEzd.dll is a common error code of integer type. Its definitions are as follow:

#define LMC1_ERR_SUCCESS			0		// Success<br />#define LMC1_ERR_EZCADRUN		1		// Find EZCAD running<br />#define LMC1_ERR_NOFINDCFGFILE	2		// Can not find EZCAD.CFG<br />#define LMC1_ERR_FAILEDOPEN		3		// Open LMC1 board failed<br />#define LMC1_ERR_NODEVICE			4		// Can not find valid lmc1 device<br />#define LMC1_ERR_HARDVER			5		// Lmc1’s version is error.<br />#define LMC1_ERR_DEVCFG 			6		// Can not find configuration files<br />#define LMC1_ERR_STOPSIGNAL		7		// Alarm signal<br />#define LMC1_ERR_USERSTOP			8		// User stops<br />#define LMC1_ERR_UNKNOW			9		// Unknown error<br />#define LMC1_ERR_OUTTIME			10		// Overtime<br />#define LMC1_ERR_NOINITIAL			11		// Un-initialized<br />#define LMC1_ERR_READFILE			12		// Read file error<br />#define LMC1_ERR_OWENWNDNULL	13		// Window handle is NULL<br />#define LMC1_ERR_NOFINDFONT		14		// Can not find designated font<br />#define LMC1_ERR_PENNO				15		// Wrong pen number<br />#define LMC1_ERR_NOTTEXT			16		// Object is not text<br />#define LMC1_ERR_SAVEFILE			17		// Save file failed<br />#define LMC1_ERR_NOFINDENT		18		// Can not find designated object<br />#define LMC1_ERR_STATUE			19		// Can not run the operation in current state

Note: The entire TCHAR object in MarkEzd.dll must be UNICODE.

<a name="QRz5I"></a>
###### lmc1_Initial
<br />INTENTION: initialize lmc1 control board<br />DEFINITION: int lmc1_Initial(TCHAR* strEzCadPath, BOOL bTestMode, HWND hOwenWnd)<br />strEzCadPath:  the full path where ezcad2.exe exists<br />bTestMode  Whether in test mode or not<br />hOwenWnd:  The window that has the focus. It is used to check the user’s stop messages.<br />DESCRIPTION: you must first call lmc1¬_Initial before other function in program.<br />RETURN VALUE: common error code

<a name="EwepV"></a>
###### lmc1_Close
	<br />INTENTION: Close lmc1 board<br />DEFINITION: int lmc1_Close();<br />DESCRIPTION: you must call lmc1_Close to close the lmc1 board when exit program.<br />RETURN VALUE: common error code

<a name="vCLgN"></a>
###### lmc1_LoadEzdFile
<br />INTENTION: open the appointed ezd file, and clear all the object in database.<br />DEFINITION: int lmc1_LoadEzdFile(TCHAR* strFileName);<br />DESCRIPTION: this function can open an ezd file that was build by user as a template. User need not set process parameters, because they will be loaded in from the template file.<br />RETURN VALUE: common error code

<a name="soUG4"></a>
###### lmc1_Mark
<br />INTENTION: mark all the data in database<br />DEFINITION: int lmc1_Mark(BOOL bFlyMark)；<br />bFlyMark= TRUE  // mark on fly<br />DISCRIPTION: Begin to mark by calling this function after loading ezd file using lmc1_LoadEzdFile. The function will not return back until marking complete.<br />RETURN VALUE: common error code

<a name="hE6tU"></a>
###### lmc1_ChangeTextByName
<br />INTENTION: change the content of the text with appointed name.<br />DEFINITION: int lmc1_ChangeTextByName(TCHAR_ strTextName, TCHAR_ strTextNew);<br />strTextName     the name of text object whose content will be changed<br />strTextNew      new content of text<br />DISCRIPTION: after loading ezd file by lmc_LoadEzdFile, user can use this function to change the content of appointed text object before marking it.

<a name="qGvHq"></a>
###### lmc1_MarkEntity
<br />INTENTION: mark the appointed named object in database<br />DEFINITION: int lmc1_MarkEntity(TCHAR* strEntName);<br />DISCRIPTION: after loading ezd file by lmc1_LoadEzdFile, user can use this function to mark the appointed object. The function will not return back until marking complete.<br />RETURN VALUE: common error code

<a name="xNuA3"></a>
###### lmc1_ReadPort
<br />INTENTION: read the input port of the lmc1<br />DEFINITION: int lmc1_ReadPort(WORD& data)；<br />data:   the data in input port<br />DISCRIPTION: call lmc1_ReadPort to read the data from input ports<br />RETURN VALUE: common error code

<a name="qy6EU"></a>
###### lmc1_WritePort
<br />INTENTION: write data to output port on the lmc1<br />DEFINITION: int lmc1_WritePort(WORD data)；<br />data: the data to output ports<br />DISCRIPTION: call lmc1_WritePort to write data to the output port<br />RETURN VALUE: common error code

<a name="yoSCP"></a>
###### lmc1_GetPrevBitmap
<br />INTENTION: Get the preview picture of all the objects in database.<br />DEFINITION: CBitmap* lmc1_GetPrevBitmap(HWND hwnd, int nBMPWidth, int nBMPHeight)；<br />Hwnd: Window Handle that the preview shows in<br />nBMPWidth: the preview picture’s width in pixel<br />nBMPHeight: the preview picture’s height in pixel<br />DISCRIPTION: Call lmc1_GetPrevBitmap to get the preview picture of all the objects in database. It can be used to refresh the interface.<br />RETURN VALUE: return picture’s pointer if successful and NULL if failed

<a name="O6jJK"></a>
###### lmc1_SetDevCfg
<br />INTENTION: set parameter for device<br />DEFINITION: int lmc1_SetDevCfg( )<br />DISCRIPTION: call lmc1_SetDevCfg, and then a window will be popup. User could set parameters of device in it.<br />RETURN VALUE: common error code

<a name="gzkgH"></a>
###### lmc1_SetHathParam
<br />INTENTION: Set the hatch parameter<br />DEFINITION: int lmc1_SetHatchParam (<br />BOOL   bEnableContour,	//enable the contour of object to be marked<br />int    bEnableHatch1, //enable hatch NO. 1<br />int    nPenNo1, //set the pen of hatch NO. 1<br />int    nHatchAttrib1, //set the attribute of hatch NO. 1<br />double dHatchEdgeDist1, //set the distance between hatch line and contour of hatch NO. 1<br />double dHatchLineDist1, //set the distance between two line of hatch NO. 1 .<br />double dHatchStartOffset1, //set the start offset of hatch NO. 1<br />double dHatchEndOffset1, //set the end offset of hatch NO. 1<br />double dHatchAngle1, //set the hatch angle of hatch NO. 1<br />int    bEnableHatch2, //enable hatch1 NO.2<br />int    nPenNo2,<br />int    nHatchAttrib2,<br />double dHatchEdgeDist2,<br />double dHatchLineDist2.<br />double dHatchStartOffset2,<br />double dHatchEndOffset2,<br />double dHatchAngle2<br />);

nHatchAttrib1: attribute of hatch，which is a combination of the following values:<br />const int HATCHATTRIB_ALLCALC = 0x01; //compute all object as one<br />const int HATCHATTRIB_BIDIR   = 0x08; // reciprocating hatch<br />const int HATCHATTRIB_EDGE    = 0x02; // re-mark the edge	<br />const int HATCHATTRIB_LOOP    = 0x10; // ring-like hatch

DISCRIPTION: call lmc1_SetHatchParam to set the parameters of hatch. The parameters will be used for the latter hatched object.<br />RETURN VALUE: common error code

<a name="WQmX3"></a>
###### lmc1_SetFontParam
<br />INTENTION: set the parameter of font<br />DEFINITION: int lmc1_SetFontParam(<br />TCHAR* strFontName<br />double dCharHeight,<br />double dCharWidth,<br />double dCharAngle,<br />double dCharSpace,<br />double dLineSpace,<br />BOOL   bEqualCharWidth<br />);<br />strFontName:   name of font<br />dCharHeight:   height of character<br />dCharWidth:   width of character<br />dCharAngle:   angle of character<br />dCharSpace:   distance between the characters<br />dLineSpace:    distance between the lines.<br />bEqualCharWidth:  enable the same characters width mode<br />DISCRIPTION: call lmc1_SetFontParam to set parameters of font. The parameters will be used for the latter text object added in database.<br />RETURN VALUE: common error code

<a name="LfT0K"></a>
###### lmc1_GetPenParam
<br />INTENTION: get the parameter of appointed pen<br />DEFINITION: int lmc1_GetPenParam(<br />int      nPenNo, 	// Pen’s NO. (0-255)<br />int&     nMarkLoop,	 //mark times<br />double&   dMarkSpeed, 	//speed of marking mm/s<br />double&   dPowerRatio,		// power ratio of laser (0-100%)	<br />double&   dCurrent,	//current of laser (A)<br />int&      nFreq,	// frequency of laser HZ<br />int&      nQPulseWidth, 	//width of Q pulse (us)	<br />int&      nStartTC,	// Start delay (us)<br />int&      nLaserOffTC,	//delay before laser off (us)<br />int&      nEndTC,		// marking end delay (us)<br />int&      nPolyTC	,	//delay for corner (us)<br />double&   dJumpSpeed, 	//speed of jump without laser (mm/s)<br />int&      nJumpPosTC, 	//delay about jump position (us)<br />int&      nJumpDistTC,	//delay about the jump distance (us)	<br />double&   dEndComp,	// compensate for end (mm)<br />double&   dAccDist,	// distance of speed up (mm)	<br />double&   dPointTime,	//delay for point mark (ms)<br />BOOL&   bPulsePointMode,	//pulse for point mark mode<br />int&      nPulseNum,	//the number of pulse<br />double&   dFlySpeed	//speed of production line<br />);<br />DISCRIPTION: call lmc1_GetParam to get the parameter of appointed pen in database<br />RETURN VALUE: common error code

<a name="X9CYw"></a>
###### lmc1_SetPenParam
<br />INTENTION: Set the pan parameter<br />DEFINITION: int lmc1_SetPenParam(<br />int      nPenNo,	 // Pen’s NO. (0-255)<br />int&      nMarkLoop,	 //mark times<br />double&   dMarkSpeed,	 //speed of marking mm/s<br />double&   dPowerRatio,	// power ratio of laser (0-100%)	<br />double&   dCurrent,	//current of laser (A)<br />int&      nFreq,	// frequency of laser HZ<br />int&      nQPulseWidth,	 //width of Q pulse (us)	<br />int&      nStartTC,	// Start delay (us)<br />int&      nLaserOffTC,		//delay before laser off (us)<br />int&      nEndTC,		// marking end delay (us)<br />int&      nPolyTC,		//delay for corner (us)<br />double&   dJumpSpeed, 	//speed of jump without laser (mm/s)<br />int&      nJumpPosTC,		//delay about jump position (us)<br />int&      nJumpDistTC,	//delay about the jump distance (us)	<br />double&   dEndComp,		//compensate for end (mm)<br />double&   dAccDist,	// distance of speed up (mm)	<br />double&   dPointTime,	//delay for point mark (ms)<br />BOOL&   bPulsePointMode,	//pulse for point mark mode<br />int&      nPulseNum,	//the number of pulse<br />double&   dFlySpeed	//speed of production line<br />);<br />DISCRIPTION: call lmc1_SetPenParam to set the parameters of appointed pen in database<br />RETURN VALUE: common error code

<a name="sK0mb"></a>
###### lmc1_ClearEntLib
<br />INTENTION: clear all object in database<br />DEFINITION: int lmc1_ClearEntLib();			<br />DISCRIPTION: call lmc1_ClearEntLib to clear all objects in database.<br />RETURN VALUE: common error code

<a name="adhsm"></a>
###### lmc1_AddTextToLib1
<br />INTENTION: add new text object into database.<br />DEFINITION: int lmc1_AddTextToLib(<br />TCHAR* pStr,<br />TCHAR* pEntName,<br />double dPosX,<br />double dPosY,<br />double dPosZ,<br />int    nAlign<br />double dTextRotateAngle,<br />int nPenNo,<br />BOOL bHatchText		//hatch the text object or not.<br />);<br />pStr:      the character string<br />pEntName: the name of character string object<br />dPosX    left-bottom point’s X coordinate of the character string object<br />dPosY    left-bottom point’s Y coordinate of the character string object<br />dPosZ    Z coordinate of the character string object<br />nAlign    align way 0－8<br />//meaning of the align way:<br />//   6 ---  5 ---  4<br />//   |            |<br />//   |            |<br />//   7     8     3<br />//   |            |<br />//   |            |<br />//   0 ----- 1 --- -- 2<br />dTextRotateAngle  rotation angle (in radian) that the character string object rotates around base point.<br />nPenNo          the number of pen to mark text<br />bHatchText       hatch the text object or not<br />DISCRIPTION: call lmc1_AddTextToLib to add  new text object into database.<br />RETURN VALUE: common error code

<a name="UpRhv"></a>
###### lmc1_AddCurveToLib
<br />INTENTION: add new curve object into database.<br />DEFINITION: int lmc1_AddCurveToLib(<br />double ptBuf[][2],	//array of the curve vertex<br />int  ptNum,	//number of the curve vertex<br />TCHAR* pEntName, 	//name of the curve object<br />int nPenNo, 	//the pen number of curve object<br />int bHatch	//hatch the curve object or not<br />);<br />DISCRIPTION: call lmc1_AddCurveToLib to add curve object into database.<br />RETURN VALUE: common error code

<a name="SiVJC"></a>
###### lmc1_AddFileToLib
<br />INTENTION: add the appointed file into database.<br />DEFINITION：int lmc1_AddFileToLib(<br />TCHAR* pFileName,	//filename<br />TCHAR* pEntName,		// name of the file object<br />double dPosX, 	// X coordinate of left-bottom point<br />double dPosY, 	// Y coordinate of left-bottom point<br />double dPosZ,	// Z coordinate of the file object<br />int    nAlign,	// align way 0－8<br />double dRatio,	// scaling ratio				<br />int nPenNo,	//the pen number of the file object<br />BOOL bHatchFile 	// hatch the file object or not<br />);

DISCRIPTION: call lmc1_AddFileLib to add new file object into database. The following file formats are supported : ezd, dxf， dst, plt, ai, bmp, jpg, tga, png, gif, tiff<br />RETURN VALUE: common error code

<a name="PRIfO"></a>
###### lmc1_AddBarCodeTolib
<br />INTENTION: add a new bar code object into database.<br />DEFINITION: int lmc1_AddBarCodeToLib(<br />TCHAR* pStr,<br />TCHAR* pEntName,<br />double dPosX,<br />double dPosY,<br />double dPosZ,<br />int    nAlign,<br />int    nPenNo,<br />int    bHatchText,<br />int    nBarcodeType,<br />WORD   wBarCodeAttrib,<br />double dHeight,<br />double dNarrowWidth,<br />double dBarWidthScale[4],<br />double dSpaceWidthScale[4],<br />double dMidCharSpaceScale,<br />double dQuietLeftScale,<br />double dQuietMidScale,<br />double dQuietRightScale,<br />double dQuietTopScale,<br />double dQuietBottomScale,<br />int    nRow,<br />int    nCol,<br />int    nCheckLevel,<br />int    nSizeMode,<br />double dTextHeight,<br />double dTextWidth,<br />double dTextOffsetX,<br />double dTextOffsetY,<br />double dTextSpace,<br />TCHAR* pTextFontName<br />);

pStr		character string of the bar code<br />pEntName  name of the bar code object<br />dPosX,  X coordinate of left-bottom basic point of the barcode<br />dPosY  Y coordinate of left-bottom basic point of the barcode<br />dPosZ  Z coordinate of the bar code object<br />nAlign, align way 0－8<br />nPenNo   the pen NO. of the barcode object<br />bHatchText  hatch the barcode object or not<br />nBarcodeType  type of barcode, see following:<br />#define BARCODETYPE_39      0<br />#define BARCODETYPE_93      1<br />#define BARCODETYPE_128A    2<br />#define BARCODETYPE_128B    3<br />#define BARCODETYPE_128C    4<br />#define BARCODETYPE_128OPT  5<br />#define BARCODETYPE_EAN128A 6<br />#define BARCODETYPE_EAN128B 7<br />#define BARCODETYPE_EAN128C 8<br />#define BARCODETYPE_EAN13   9<br />#define BARCODETYPE_EAN8    10<br />#define BARCODETYPE_UPCA    11<br />#define BARCODETYPE_UPCE    12<br />#define BARCODETYPE_25      13<br />#define BARCODETYPE_INTER25 14<br />#define BARCODETYPE_CODABAR 15<br />#define BARCODETYPE_PDF417  16<br />#define BARCODETYPE_DATAMTX 17<br />wBarCodeAttrib attribute of barcode.<br />#define BARCODEATTRIB_REVERSE		0x0008	// reverse barcode<br />#define BARCODEATTRIB_HUMANREAD	0x1000 // show the character<br />#define BARCODEATTRIB_CHECKNUM	0x0004 // need check number<br />#define BARCODEATTRIB_PDF417_SHORTMODE		0x0040 //short mode of PDF417<br />#define BARCODEATTRIB_DATAMTX_DOTMODE	0x0080 //point mode of DataMtrix

dHeight        height of bar code 	<br />dNarrowWidth: width of the narrowest module<br />dBarWidthScale: ratio of bar width to narrowest module<br />dSpaceWidthScale: ratio of space width to the narrowest module<br />dMidCharSpaceScale ratio of character space width to the narrowest module<br />dQuietLeftScale: ratio of the left blank width to the narrowest module<br />dQuietMidScale: ration of the middle blank width to the narrowest module<br />dQuietRightScale: ratio of the right blank width to the narrowest module<br />dQuietTopScale: ratio of the top blank width to the narrowest module<br />dQuietBottomScale: ratio of the bottom blank width to the narrowest module<br />nRow:  row number of two-dimension barcode<br />nCol:  column number of two-dimension barcode<br />nCheckLevel, //pdf417 error recovery level 0-8<br />nSizeMode, //DataMatrix size mode 0-30<br />#define DATAMTX_SIZEMODE_SMALLEST  0<br />#define DATAMTX_SIZEMODE_10X10     1<br />#define DATAMTX_SIZEMODE_12X12     2<br />#define DATAMTX_SIZEMODE_14X14     3<br />#define DATAMTX_SIZEMODE_16X16     4<br />#define DATAMTX_SIZEMODE_18X18     5<br />#define DATAMTX_SIZEMODE_20X20     6<br />#define DATAMTX_SIZEMODE_22X22     7<br />#define DATAMTX_SIZEMODE_24X24     8<br />#define DATAMTX_SIZEMODE_26X26     9<br />#define DATAMTX_SIZEMODE_32X32     10<br />#define DATAMTX_SIZEMODE_36X36     11<br />#define DATAMTX_SIZEMODE_40X40     12<br />#define DATAMTX_SIZEMODE_44X44     13<br />#define DATAMTX_SIZEMODE_48X48     14<br />#define DATAMTX_SIZEMODE_52X52     15<br />#define DATAMTX_SIZEMODE_64X64     16<br />#define DATAMTX_SIZEMODE_72X72     17<br />#define DATAMTX_SIZEMODE_80X80     18<br />#define DATAMTX_SIZEMODE_88X88     19<br />#define DATAMTX_SIZEMODE_96X96     20<br />#define DATAMTX_SIZEMODE_104X104   21<br />#define DATAMTX_SIZEMODE_120X120   22<br />#define DATAMTX_SIZEMODE_132X132   23<br />#define DATAMTX_SIZEMODE_144X144   24<br />#define DATAMTX_SIZEMODE_8X18     25<br />#define DATAMTX_SIZEMODE_8X32     26<br />#define DATAMTX_SIZEMODE_12X26     27<br />#define DATAMTX_SIZEMODE_12X36     28<br />#define DATAMTX_SIZEMODE_16X36     29<br />#define DATAMTX_SIZEMODE_16X48     30<br />dTextHeight  height of the character string<br />dTextWidth width of the character string<br />dTextOffsetX  X offset of the character string<br />dTextOffsetY  Y offset of the character string<br />dTextSpace  space of the character string<br />pTextFontName  font name of the character string<br />DISCRIPTION: call lmc1_AddBarCodeToLib to add bar code object into database.<br />RETURN VALUE: common error code

<a name="z6J0z"></a>
###### lmc1_SetRotateParam
<br />INTENTION: set parameter for rotation transform<br />DEFINITION：int lmc1_SetRotateParam(double dCenterX, double dCenterY, double dRotateAng)；			<br />dCenterX:  X coordinate of rotate center<br />dCenterY:  Y coordinate of rotate center<br />dRotateAng:  rotation angle (in radian)<br />DISCRIPTION: call lmc1_SetRotateParam to set the parameter of rotation transform. All of the objects in database are rotated around the appointed center.<br />RETURN VALUE: common error code

<a name="MyRKz"></a>
###### lmc1_AxisMoveTo
<br />INTENTION: move the extended axis to appointed position.<br />DEFINITION:int lmc1_AxisMoveTo(int axis,double GoalPos)；<br />axis     axis number  0 = axis 0  1 = axis 1<br />GoalPos: absolute coordinate of position<br />DISCRIPTION: call lmc1_AxisMoveTo to move extended axis to the appointed absolute coordinate position. The moving speed is the biggest speed set in parameter.<br />RETURN VALUE: common error code

<a name="lQrS1"></a>
###### lmc1_AxisCorrectOrigin
<br />INTENTION: calibrate the origin of extended axis<br />DEFINITION：int lmc1_AxisCorrectOrigin(int axis)；<br />axis     axis number  0 = axis 0  1 = axis 1<br />DISCRIPTION: call lmc1_AxisCorrectOrigin to calibrate the origin of extended axis automatically<br />RETURN VALUE: common error code

<a name="a9nFt"></a>
###### lmc1_GetAxisCoor
<br />INTENTION: get the coordinate of extended axis.<br />DEFINITION: int lmc1_GetAxisCoor(int axis)；<br />axis:     axis number  0 = axis 0  1 = axis 1<br />DISCRIPTION: call lmc1_GetAxisCoor to get the coordinate of extended axis.<br />RETURN VALUE:  coordinate of appointed extended axis

<a name="DmhO4"></a>
###### lmc1_Reset
<br />INTENTION: enable and reset the coordinate of extend axis<br />DEFINITION: int lmc1_Reset(BOOL bEnAxis0 , BOOL bEnAxis1)；<br />bEnAxis0    enable extended axis 0 or not<br />bEnAxis1    enable extended axis 1 or not<br />DISCRIPTION: Before calling any other function about extended axis, you must call lmc1_Reset first to enable the appointed axis. When the extended axis moves to the limited position, lmc1_Reset can be called to reset the coordinate.<br />RETURN VALUE: common error code

<a name="bf2PU"></a>
###### lmc1_GetAllFontRecord
<br />INTENTION: get the parameters of all fonts that are supported by system.<br />DEFINITION: lmc1_FontRecord* lmc1_GetAllFontRecord(int& nFontNum)；<br />nFontNum  the number of fonts<br />//Font type definition<br />#define FONTATB_JSF        0x0001        //JczSingle type<br />#define FONTATB_TTF        0x0002        //TrueType type<br />#define FONTATB_DMF        0x0004        //DotMatrix type<br />#define FONTATB_BCF        0x0008        //BarCode type<br />//Font record<br />struct lmc1_FontRecord<br />{  	<br />TCHAR   szFontName[256];     //name of font<br />DWORD   dwFontAttrib;       //attribute of font<br />};

DISCRIPTION : get the parameters of all fonts that are supported by system.<br />RETURN VALUE: pointer of array of fonts recording

<a name="IQapA"></a>
###### lmc1_SaveEntLibToFile
<br />INTENTION: save all objects in database to the appointed .ezd file.<br />DEFINITION: int lmc1_SaveEntLibToFile(TCHAR* strFileName)；<br />strFileName    name of ezd file<br />DISCRIPTION: save all objects in database to the appointed ezd file.<br />RETURN VALUE: common error code

<a name="KohyS"></a>
###### lmc1_GetEntSize
<br />INTENTION: get the maximum and minimal coordinate of the appointed object.<br />DEFINITION: int lmc1_GetEntSize(TCHAR* pEntName,<br />double& dMinx,<br />double& dMiny,<br />double& dMaxx,<br />double& dMaxy ,<br />double& dZ)；<br />pEntName  name of object<br />dMinx  minimal coordinate X<br />dMiny  minimal coordinate Y<br />dMaxx  maximum coordinate X<br />dMaxy  maximum coordinate Y<br />dZ      coordinate Z

DISCRIPTION: get the maximum and minimal coordinate of the appointed object.<br />RETURN VALUE: common error code

<a name="olMg0"></a>
###### lmc1_MoveEnt
<br />INTENTION: move object appointed distance<br />DEFINITION: int lmc1_GetEntSize(TCHAR* pEntName,<br />double dMovex,<br />double dMovey)；<br />pEntName: name of object<br />dMovex: the X distance of object moving<br />dMovey: the Y distance of object moving

DISCRIPTION: move object appointed distance<br />RETURN VALUE: common error code

<a name="rufF8"></a>
###### lmc1_RedLightMark
<br />INTENTION: mark the contour using indicated red light<br />DEFINITION: int lmc1_RedLightMark();<br />DISCRIPTION: mark the contour using indicated red light<br />RETURN VALUE: common error code

<a name="YBoXX"></a>
###### lmc1_MarkLine
<br />INTENTION: mark the appointed line<br />DEFINITION: int lmc1_MarkLine(double x1,<br />double y1<br />double x2,<br />double y2,<br />int pen)；<br />x1, y1: the coordinate of the starting point<br />x2, y2: the coordinate of end point<br />pen:  Pen NO.<br />RETURN VALUE: common error code

<a name="XW7Bm"></a>
###### lmc1_MarkPoint
<br />INTENTION: mark the appointed point<br />DEFINITION：int lmc1_MarkPoint(double x,<br />double y<br />double delay,<br />int pen)；<br />x,y: the coordinate of point<br />delay: marking time<br />pen:  Pen NO.<br />DISCRIPTION: mark a point at the appointed station.<br />RETURN VALUE: common error code

<a name="Kdify"></a>
###### lmc1_GetCurCoor
<br />INTENTION: get the coordinate of scan head<br />DEFINITION: ：int lmc1_GetCurCoor(double& x, double& y)；<br />x,y:  current coordinate of scan head<br />DISCRIPTION: get the coordinate of scan head<br />RETURN VALUE: common error code

<a name="RBJl9"></a>
###### lmc1_GetEntityCount
<br />INTENTION: get the total number of objects in database.<br />DEFINITION: int lmc1_GetEntityCount()；<br />DISCRIPTION: get the total number of objects in database.<br />RETURN VALUE:  Total count of object in database

<a name="M8pSK"></a>
###### lmc1_GetEntityName
<br />INTENTION: get the name of the object that has appointed serial number<br />DEFINITION: int lmc1_GetEntityName(int nEntityIndex,<br />TCHAR szEntName[256])；<br />NEntityIndex: appoint the serial number， 0－(total number-1). The total objects count can be got by lmc1_GetEntityCount.<br />szEntName: name of appointed object<br />DISCRIPTION: get the name of the object that has appointed serial number<br />RETURN VALUE: common error code

<a name="aB0y8"></a>
# DEVELOPMENT STEPS
<br />We will show an example about how to do the Development

Client need mark one line text in a rectangle, which is shown as following, and the content of text must be achieved from a network server.

Common step of Development as follows:<br />Step 1. Create a template file as test.ezd, then create a new text object and named it to “name”. Adjust the size, position and parameters to reach the machining effect. Then save file and exit EzCad2.

Step 2.  Program software for calling markezd.dll.<br />a)	First step : Dynamic Load MarkEzd.dll<br />HINSTANCE hEzdDLL = LoadLibrary(_T("MarkEzd.dll"));

b)	Second step:  get the pointer of the function to be called

lmc1_Initial=(LMC1_INITIAL)GetProcAddress(hEzdDLL, _T("lmc1_Initial"));<br />lmc1_Close=(LMC1_CLOSE)GetProcAddress(hEzdDLL, _T("lmc1_Close"));<br />lmc1_LoadEzdFile=(LMC1_LOADEZDFILE)GetProcAddress(hEzdDLL,_T("lmc1_LoadEzdFile"));	<br />lmc1_Mark=(LMC1_MARK)GetProcAddress(hEzdDLL,_T("lmc1_Mark"));<br />lmc1_ChangeTextByName=(LMC1_CHANGETEXTBYNAME)GetProcAddress(hEzdDLL,_T("lmc1_ChangeTextByName"));	<br />c)	Third step: Call the function<br />1）	Initialization lmc1 board:  lmc1_Initial()<br />2）	Open test.ezd: lmc1_LoadEzdFile(_T(“test.ezd”)).<br />3）	Get the text content from network server. User must write this segment program oneself.<br />4）	Change the content of the named text object.<br />lmc1_ChangeTextByName (_T(“name”)， szTextAchievedFromNetwork);<br />5）	Call lmc1_Mark() for machining<br />6）	If go on, return to 3).<br />7）	Close lmc1 board: lmc1_Close().

d)	Fourth step, Release markezd.dll: FreeLibrary(hEzdDLL)

Appendix: Set project to Unicode type in VC++

1.  Choose “Microsoft Visual C++ 6.0” when install visual studio, and click “Change Option”. 
2.  Choose “VC++ MFC and Template Libraries” and click “Change Option”. 
3.  Choose “MS Foundation Class Libraries” and click “change option”. 
4.  Choose the options as following picture, and click “OK”. 
5.  Open the project, choose menu Project->Settings. Choose “C/C++”, add “UNICODE” and delete “MCBS” in “Preprocessor definitions” 
6.  Choose “Link”, select “Output” in Category, and add “wWinMainCRTStartup” in “Entry-point symbol” 
7.  Change all “char” to “TCHAR” in source code. 
8.  Change all character string included by double quotation marks “…” to _T(“…”) 
9.  Compile and link the project again. 
