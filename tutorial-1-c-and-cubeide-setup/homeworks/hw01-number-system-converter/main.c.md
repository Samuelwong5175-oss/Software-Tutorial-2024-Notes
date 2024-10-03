# Skeleton Code

> Please don't include any extra libraries in your homework. We already included
> all necessary libraries in the skeleton code.

```c
#include <stdio.h>
#include <string.h>
#include <stdint.h>
#include <stdbool.h>

const char* const error_msg_decimal = "Error! That set of number is not a decimal number.\n";
const char* const error_msg_trinary = "Error! That set of number is not a trinary number.\n";
const char* const error_msg_duodecimal = "Error! That set of number is not a duodecimal number.\n";
const char* const error_msg_unsupported_system = "Error! The number system is not supported.\n";

const char* const msg_prompt_number = "Please enter a set of number:\n";
const char* const msg_prompt_current_number_system = "Please enter the current number system:\n";
const char* const msg_prompt_number_system_to_convert = "Please enter the number system you want the set of number be converted to:\n";
const char* const msg_output = "Output=";

int main(){
  
  
    printf("%s", msg_prompt_number);
  
    /**
     * @brief 
     * Get user input for number to be convert
     */
// Allocating memory for 100 characters
    char* str = (char*)malloc(100 * sizeof(char));  
    
    // Check if memory was successfully allocated
    if (str == NULL) {
        printf("Memory allocation failed!\n");
        return 1; // Exit if allocation fails
    }
// Allocating memory for 100 characters

    scanf("%s", &str);

// Check number is valid or not
    for (int i = 0; str[i] != '\0'; i++) {
        if (!((str[i] >= '0' && str[i] <= '9') || (str[i] >= 'A' && str[i] <= 'B') || (str[i] >= 'a' && str[i] <= 'b'))){
            return;
        }
    }
// Check number is valid or not


    // TODO:

    printf("%s", msg_prompt_current_number_system);
    
    /**
     * @brief 
     * Get user input for current number system
     */
    int numsys;
    scanf("%d", numsys);

    if ((numsys != 3) || (numsys != 10) || (numsys != 12)) {
        printf("%s", error_msg_unsupported_system);
        return;
    }

    if (numsys == 3){
        for (int i = 0; str[i] != '\0'; i++) {
            if (!(str[i] >= '0' && str[i] <= '2')) {
                printf(%s, error_msg_trinary);
                return;
            }
        }     
    }
    else if (numsys == 10){
        for (int i = 0; str[i] != '\0'; i++) {
            if (!(str[i] >= '0' && str[i] <= '9')) {
                printf(%s, error_msg_decimal);
                return;
            }     
        }
    }
    else if (numsys == 12){
        for (int i = 0; str[i] != '\0'; i++) {
            if (!((str[i] >= '0' && str[i] <= '9') || (str[i] >= 'A' && str[i] <= 'B') || (str[i] >= 'a' && str[i] <= 'b'))) {
                printf(%s, error_msg_duodecimal);
                return;
            }     
        }
    }
    // TODO:
    printf("%s", msg_prompt_number_system_to_convert);

    /**
     * @brief 
     * Get user input for the number system for conversion.
     * Print converted number in format of "Output=12", e.g Output=ABCDEF
     * No space should be inserted in the asnwer "Output=XXX".
     * In case of wrong number system for conversion, please use the above error msgs.
     */

    // TODO:


    return 0;
}
// C programmers never die. They are just cast into void.
```
