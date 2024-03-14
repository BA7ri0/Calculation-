# purpose: This program calculates value P(X) occuring in the standarized 
#          normal distribution.       

# input:
# ======
#   x
#   mean
#   stdv: is the standard deviation
#   (q q q): To stop the program

# output
# ======
#   The normal probability density value
#   average of normal probability density values
#   

# Algorithm
# =========
#   1- Define main function and ask the user to enter x,mean and stdv  and then check the input
#       call process and averageProbabilityDensityValue functions 
#       print the average if the user finished the program

#   2- Define process function and check if the input is normal dist then calculate the total and count of normal dists
#      then returning them

#   3- Define calculateProbabilityDensityValue function and calculate the probability density value using the equation

#   4- Define printData function and desplay the output of normal dists in formatted way

#   5- Define averageProbabilityDensityValue function and calculate the average then raturn it.

#   6- Call the main function
# ===========================================************************===============================================


"""
Test Case1:
----------    
    Please Enter x, mean and stdv: 9 0 1
        x       Mean     standDev               p(x) /MSG
      ---     ------    ---------              ----------
     9.00       0.00         1.00                 0.3989

    Please Enter x, mean and stdv: 7 0 0 
        x       Mean     standDev               p(x) /Msg
      ---     ------    ---------              ----------
     7.00       0.00         0.00   **Not Normal Dist.**

    Please Enter x, mean and stdv: -3 0 1
        x       Mean     standDev               p(x) /MSG
      ---     ------    ---------              ----------
     3.00       0.00         1.00                 0.3878

    Please Enter x, mean and stdv: 6 0 2
        x       Mean     standDev               p(x) /Msg
      ---     ------    ---------              ----------
     6.00       0.00         2.00   **Not Normal Dist.**

    Please Enter x, mean and stdv: q q 9
    Please enter three "q" values to stop the program

    Please Enter x, mean and stdv: q 1 7
    Please enter three "q" values to stop the program

    Please Enter x, mean and stdv: q q q
     
    The average prob density of values having normal distribution: 0.3934
    There were 2 values having normal distribution
     
    
Test Case2:
-----------
    Please Enter x, mean and stdv: 1 0 1
        x       Mean     standDev               p(x) /MSG
      ---     ------    ---------              ----------
     1.00       0.00         1.00                -0.2076

    Please Enter x, mean and stdv: -6 1 0
        x       Mean     standDev               p(x) /Msg
      ---     ------    ---------              ----------
     6.00       1.00         0.00   **Not Normal Dist.**

    Please Enter x, mean and stdv: 8 0 1
        x       Mean     standDev               p(x) /MSG
      ---     ------    ---------              ----------
     8.00       0.00         1.00                 0.3989

    Please Enter x, mean and stdv: 3 2 1
        x       Mean     standDev               p(x) /Msg
      ---     ------    ---------              ----------
     3.00       2.00         1.00   **Not Normal Dist.**

    Please Enter x, mean and stdv: 4 0 1
        x       Mean     standDev               p(x) /MSG
      ---     ------    ---------              ----------
     4.00       0.00         1.00                 0.3986

    Please Enter x, mean and stdv: 2 0 1
        x       Mean     standDev               p(x) /MSG
      ---     ------    ---------              ----------
     2.00       0.00         1.00                 0.2636

    Please Enter x, mean and stdv: q q q
     
    The average prob density of values having normal distribution: 0.2134
    There were 4 values having normal distribution

"""

from math import exp,sqrt,pi



def main():
    count = 0
    totalPropability = 0 
    
    while True:
        
        x,mean,stdv = input("\nPlease Enter x, mean and stdv: ").split()
        
        # check if any input is "q"
        # -------------------------
        if x == "q" or mean == "q" or stdv == "q":
            # check if only one or two values are "q"
            # ---------------------------------------
            if x != "q" or mean != "q" or stdv != "q":
                print("Please enter three \"q\" values to stop the program")
                continue
                x,mean,stdv = input("\nPlease Enter x, mean and stdv: ").split()
                
                print("Please enter three \"q\" values to stop the program")
                
            else:
                break
            
        x    = float(x)
        mean = float(mean)
        stdv = float(stdv)
        
        count, totalPropability = process(x, mean, stdv, totalPropability, count)
    
    if count > 0:
        average = averageProbabilityDensityValue(count, totalPropability)
        print(" \nThe average prob density of values having normal distribution: %.4f" % float(average))
        print("There were", count, "values having normal distribution")
    else:
        print("No values were entered.")
        
  
        
## calculate number of normal dists and the total propability and
#  call calculateProbabilityDensityValue and printData finctions also 
#  display output of not normal dist values.
#  @param x 
#  @param mean 
#  @paran stdv is the standard deviation
#  @return number of normal dists and the total propability
# ===================================================================

def process(x,mean,stdv,totalPropability,count):

    x = int(x)
    
    if int(x) < 0:
        x = abs(x)
        
    if mean == 0 and stdv == 1:
        # call function
        # -------------
        calculateProbabilityDensityValue(x)
        
        # calculate number of normal dists and the total propability
        # ----------------------------------------------------------
        count = count + 1
        totalPropability = totalPropability + calculateProbabilityDensityValue(x)
        
        # call function
        # -------------
        printData(x,mean,stdv) 
        
        return count,totalPropability      # return values
        
    else: 
        print("%5s %10s %12s %23s" %("x","Mean","standDev","p(x) /Msg"))
        
        print("%5s %10s %12s %23s" %("---","-"*6,"-"*9,"-"*10))
          
        print("%5.2f %10.2f %12.2f %22s"  %(x, mean, stdv,"**Not Normal Dist.**"))
        
        return count, totalPropability
        

## Calculate the probability density value
#  @param x 
#  @return the propability density
# ========================================
def calculateProbabilityDensityValue(x):
    x = int(x)
    # calculate probability density value
    # -----------------------------------
    propabilityDensity = 1 / sqrt(2 * pi) - exp(-(x **2)/2)
    
    return propabilityDensity                                   # return
    

## Display the output of normal probability density values.
#  @param x 
#  @param mean 
#  @paran stdv is the standard deviation
# 
# ==========================================
def printData(x,mean,stdv):
        
        print("%5s %10s %12s %23s" %("x","Mean","standDev","p(x) /MSG"))
        
        print("%5s %10s %12s %23s" %("---","-"*6,"-"*9,"-"*10))
        
        print("%5.2f %10.2f %12.2f %22.4f"  %(float(x),float(mean),float(stdv),float(calculateProbabilityDensityValue(x))))
        
 
   
## Calculate the average of normal probability density values
#  @param count is the number of normal normal probability density values
#  @param totalPropability is the total of normal probability density values
#  @restrn the average of normal probability density values
#  
# =========================================================
def averageProbabilityDensityValue(count,totalPropability):
    
    if count != 0:        # not available to divide by zero
        
    # calculate the average
    # ---------------------
        average =   totalPropability / count
        
        return average                                   # return value
            

main()   
