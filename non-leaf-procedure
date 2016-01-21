.data											#define variable that will be stored in Static memory location

prompt: .asciiz "Enter number\n"				#string
result: .asciiz "Result: \n"					#string
comma: .asciiz ", "								#string


.text											#alphanumeric identifier
.globl main										#make global for external use
	
main:											#beginning of code

	li $v0, 4 									#referencing the print_string system call (4)
	la $a0, prompt								#passing string
	syscall										#execute

	li $v0, 5									#system call code for user input in integer, i.e., read_int
	syscall										#excute the read_int system call

	move $t3, $v0								#moving number of iterations to t3
	li $a1, 1									#input = 1

	li $v0, 4 									#referencing the print_string system call (4)
	la $a0, result								#passing string
	syscall										#execute

	j loop										#enter loop

loop:											#for (a1 = 1, a1 < t0, a1++)

	slt $t1, $a1, $t3							#if a1 < max, t1 = 1, else t1 = 0
	beq $t1, $zero, exit						#if t1 == 0 we are done with loop

	jal factorial								#jump and link to factorial loop

	move $t2, $v1								#saving result in t2

	li $v0, 1									#referencing print int system call
	move $a0, $t2								#passing value to print int system call
	syscall										#execute print

	li $v0, 4 									#referencing the print_string system call (4)
	la $a0, comma								#passing string
	syscall										#execute

	addi $a1, $a1, 1							#a1++

	j loop										#return to top of loop

exit:											#exit function

	li $v0, 10 									#referencing exit function
	syscall										#execute exit

factorial:										#beginning of factorial function

	addi $sp, $sp, -8							#adjusting stack
	sw $a1, 0($sp)								#saving argument to stack
	sw $ra, 4($sp)								#saving input to stack

	slti $t0, $a1, 1							#if n < 1 this is not base case
	beq $t0, $zero, recur						#so jump to recursive step

	li $v1, 1									#base case = 1
	addi $sp, $sp, 8							#adjust stack

	jr $ra										#return

recur:											#recur until hitting base case

	addi $a1, $a1, -1							#if n >= 1 set argument to n - 1
	jal factorial								#and then recur

	lw $a1, 0($sp)								#just returned from jal, getting back saved argument
	lw $ra, 4($sp)								#getting back return address
	addi $sp, $sp, 8							#adjusting stack

	mul $v1, $v1, $a1							#v1 = a1 * v1, where v1 is the value we just got from the last iteration of factorial
	jr $ra										#return with final value saved in v1
