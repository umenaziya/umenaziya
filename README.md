
import time
from datetime import datetime

def printDateTime():
    
    ## This function returns current data and time
    now = datetime.now()
    dt_string = now.strftime("%d/%m/%Y %H:%M:%S")
    print("You Perfomed Operation at Date,Time:",dt_string)
    return dt_string

def countCurrency(amount): 
    # input amount int 
    # Function returns the Denominations of amount in terms of Rs.500, 200 and 100 
    # Logic = Recursive 
	notes = [ 500, 200, 100]
	notesCount = {}
	real=amount
	
	for note in notes:
		if amount >= note:
			notesCount[note] = amount//note
			amount = amount % note
			
	print ("Currency Count -> for amount: ",real)
	for key, val in notesCount.items():
		print("Rs.",key," -- ",val,sep="")
		
def numberToWords(num) :
    # Input num int 
    # Function returns the amount num in english word 
    # example : 512 as five Hundred twelve
    mapping = {
      1000000000: 'Billion',
      1000000: 'Million',
      1000: 'Thousand',
      100: 'Hundred',
      90: 'Ninety',
      80: 'Eighty',
      70: 'Seventy',
      60: 'Sixty',
      50: 'Fifty',
      40: 'Forty',
      30: 'Thirty',
      20: 'Twenty',
      19: 'Nineteen',
      18: 'Eighteen',
      17: 'Seventeen',
      16: 'Sixteen',
      15: 'Fifteen',
      14: 'Fourteen',
      13: 'Thirteen',
      12: 'Twelve',
      11: 'Eleven',
      10: 'Ten',
      9: 'Nine',
      8: 'Eight',
      7: 'Seven',
      6: 'Six',
      5: 'Five',
      4: 'Four',
      3: 'Three',
      2: 'Two',
      1: 'One'
    }
    if num==0:
        return "Zero"
    result=""
    
    for value, name in mapping.items():
        count=0
        if num>=value:
          count=num//value
          num%=value
          if count>1 or value>=100:
              result= result+" "+numberToWords(count)+" "+name
          else:
              result+=" "+name
    result=result[1:]
    return result
database={"Naziya":[0000,200000,False,[]],"Prachi Pukki":[1111,30,False,[]],"Nisha":[2222,40000,False,[]],"Sajjad":[3333,50000,False,[]]}

while True:
    print()
    stay=input("Do you want to access user or quit --> ")
    print()
    if(stay=='Quit'):
        break 
    print("Please Wait For 2 Seconds, Logging In ")
    print()
    time.sleep(2)

    name=input("Hello User, Please Enter You Id: ")
    print("Dear "+name+', Please insert your ATM Card & wait for 4 Seconds to Validate')
    time.sleep(4)
    pin = int(input('Enter your 4 digit ATM Pin: '))

    if(name in database):
        realpin=database[name][0]
        balance = database[name][1]
        frozen=database[name][2]
        
        if pin == realpin:
            if(frozen==False):
                while True:
                    
                    print()
                    print()
                    print("Press Key 1 to Check Balance")
                    print("Press Key 2 to Withdraw Money")
                    print("Press Key 3 to Deposit Money")
                    print("Press Key 4 to Exit")
                    print("Press Key 5 to Show All Denominations")
                    print("Press Key 6 to Freeze the Account")
                    print("Press Key 7 to Print Mini-Statement")

                    print()
                    print()
                    try:
                        print()
                        option = int(input('Choose any of the above options: '))
                        print()
                    except:
                        print("Please choose the valid option")
                    if option == 1:
                        dt=printDateTime()
                        print('----------------------------------')
                        
                        print(f'Your current balance is {numberToWords(balance)}')
                    if option == 2:
                        withdraw_money = int(input('Enter the Withdraw Amount In 100s Denomination: '))
                        if(withdraw_money%100==0):
                            if withdraw_money < balance:
                                balance = balance - withdraw_money
                                dt=printDateTime()
                                
                                print('----------------------------------')
                                print(f'{numberToWords(withdraw_money)} is debited from your account')
                                database[name][3].append(['Withdraw',withdraw_money,dt])
                                print(f'Your current balance is {numberToWords(balance)}')
                            else:
                                print('You do not have sufficient balance')
                        else:
                            print("Please Enter Again the Withdraw Amount in 100s Denominations")
                    if option == 3:
                        deposit_money = int(input('Enter the deposit amount: '))
                        balance = balance + deposit_money
                        dt=printDateTime()
                        print('----------------------------------')
                        
                        print(f'{numberToWords(deposit_money)} is credited to your account')
                        database[name][3].append(['Deposit ',deposit_money,dt])
                        
                        print(f'Your current balance is {numberToWords(balance)}')
                    if option == 4:
                        print('Thank you for visiting our ATM Machine...See you Again')
                        break
                    if(option==5):
                        dt=printDateTime()
                        print('----------------------------------')
                        
                        countCurrency(balance)
                    if(option==6):
                        dt=printDateTime()
                        print('----------------------------------')
                        
                        print("This Account is Freezed")
                        database[name][2]=True
                        break
                    if(option==7):
                        dt=printDateTime()
                        print('----------------------------------')
                        
                        print("Below is the Transactional History")
                        print()
                        for i,j,k in database[name][3]:
                            print("Time = ",k," ",i," amount = ","Rs.",j)
                        print()
                            
                        
        
            else:
                print('----------------------------------')
                print()
                print("This Account is Freezed Due to Security Reasons")
        
        else:
            print('You entered the wrong pin...Try Again')
    else:
        print("You Dont have an account in our bank")

          
    
# import shutil

# columns = shutil.get_terminal_size().columns
# print("hello world".center(columns))
