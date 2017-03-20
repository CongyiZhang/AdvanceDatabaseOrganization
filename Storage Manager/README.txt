*******************************************************************
Simple Storage Manager - Assignment 1
*******************************************************************

*******************************************************************
Introduction
*******************************************************************
Storage manager is an application which handles Create, Open, Close, Destroy and all the read/write
funtionalities to the files that are stored in the disk.


*******************************************************************
Data Structure
*******************************************************************
SM_FileHandler:
	fileName - a pointer that contains the fileName that is opened (default : NULL)
	totalNumPages - It denotes the number of pages in a file of size PAGE_SIZE and the range of this variable is 1 to N (default : 0)
	curPagePos - It denotes the present page in which the file descriptor is pointing to and ranges from 0 to N (default : 0)
	mgmtInfo - It is a pointer which holds the file descriptor which hold the reference to the opened file (default : NULL)

*******************************************************************
Method description
*******************************************************************
Our implimentation approach towards above functionalities are as follows

initStorageManager
-Initializes the program and denotes the start of the application

createPageFile
- Checks if the file name as the parameter is valid.
- Creates the file and checks for its successfull execution
- If the file is created successfully then fills the complete first page with "\0"
- Once the above file is filled with "\0" then the file descriptor is stored in mgminfo of SM_fileHandler
  for further reference and is kept until the method closePageFile is called

openPageFile
- opens the file in read write mode and checks is this execution was successfull
- If the file was opened successfully then the SM_FileHandler is updated with the respective informations
- Last byte location of the file is found by using seek n tell methods using which the total number of pages
  are determined.
- This information is also inturn stored in the SM_fileHandler
- The mgmInfo is again updated and file is not closed

ClosePageFile
- Checks if the fileHandler that is sent as a parameter is a valid parameter and if it is valid then the 
  mgminfo member variable is extracted and is closed as it contains the file descriptor of the file that
  was being used throughout the application
- fileHandle is made null and is made available for further file usage

DestroyPageFile
- Checks if the fileName that is sent is valid and not null
- If that is valid then the filename is removed and checked for its successfull execution

readBlock
- Check the validitiy of Filehandler and mgminfo
- Check if the pageNumber which is sent as a parameter is not greater than totalNumberOfPages in the SM_FileHandler
- Traverse through the file to the pagenumber requested and read the block and store the data in mempage variable
  which is again sent as a parameter
- mgminfo is again updated in the FileHandler as the file cursor is updated everytime a page is read, wrote or
  traversed through

getBlockPos
- Checks the validity of the SM_FileHandler
- Checks if totalPages in the file is greater than zero
- returns the value of the curPagePos in the filehandler

readFirstBlock 
- Checks the validity of the SM_FileHandler and mgmInfo in the Handler
- Resets the file cursor to the beginning of the file irrespective of where the file cursors present location is
- Once the location is set the first page is read and the data read is stored in mempage which is also a variable
  that is sent as a parameter
- curPagePos is updated to the 2nd page once this is completed

readPreviousBlock 
- Checks the validity of the SM_FileHandler and mgmInfo in the Handler
- Postion of the first byte of the previous page is calculated using PAGE_SIZE and curPagePos
- Position of cursor is set to the previously calculated byte location.
- Once the location is set the page is read and the data read is stored in mempage which is also a variable
  that is sent as a parameter

readCurrentBlock
- Checks the validity of the SM_FileHandler and mgmInfo in the Handler
- The block at which the cursor lies is read to a variable which is sent as a parameter to the method
- Once the location is set the page is read and the data read is stored in mempage which is also a variable
  that is sent as a parameter
- curPagePos is updated by incrementing it by 1

readNextBlock 
- Checks the validity of the SM_FileHandler and mgmInfo in the Handler
- Postion of the first byte of the next page is calculated using PAGE_SIZE and curPagePos
- Position of cursor is set to the previously calculated byte location.
- Once the location is set the page is read and the data read is stored in mempage which is also a variable
  that is sent as a parameter
- curPagePos is updated by incrementing it by 2

readLastBlock 
- Checks the validity of the SM_FileHandler and mgmInfo in the Handler
- Resets the file cursor to the end of the file irrespective of where the file cursors present location is
- Once the byte position of the end of file is determined then the file is decremented by PAGE_SIZE value
  to determine first byte location of last page
- Last page data is read and stored in mempage variable which is sent as a parameter to method
- curPagePos is updated to the TotalPageNumber value once this is completed

writeBlock 
- Check the validitiy of Filehandler and mgminfo
- Check if the pageNumber which is sent as a parameter is not greater than totalNumberOfPages in the SM_FileHandler
- Traverse through the file to the pagenumber requested and write to the block the data that is present in mempage variable
  which is sent as a parameter
- mgminfo is again updated in the FileHandler as the file cursor is updated everytime a page is read, wrote or
  traversed through

writeCurrentBlock
- Checks the validity of the SM_FileHandler and mgmInfo in the Handler
- The block at which the cursor lies is read to a variable which is sent as a parameter to the method
- Once the location is set the page is read and the data read is stored in mempage which is also a variable
  that is sent as a parameter
- curPagePos is updated by incrementing it by 1

appendEmptyBlock 
- Checks the validity of the Sm_FileHandler and mgmInfo in the handler
- The File cursor is traversed to the end of file and then an empty page is added and is filled with "\0" characters
- The Success of the above execution is verified 
- TotalNumberOfPages is incremented by 1 value

ensureCapacity 
- Checks the validity of the Sm_FileHandler and mgmInfo in the handler
- Initiates a while loop which terminates when the SM_FileHandler-totalNumPages becomes equal to numberOfPages which 
  is an integer values sent as a parameter to the method
- Inside the while loop appendEmptyBlock function call is made which ensure those many number of pages are added which
  inturn ensures the requred number of pages exists