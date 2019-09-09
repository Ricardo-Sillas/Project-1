# Project-1
import hashlib

def hash_with_sha256(str):
    hash_object = hashlib.sha256(str.encode('utf-8'))
    hex_dig = hash_object.hexdigest()
    return hex_dig

# starts numbers off with length 3, increments the number by one, then increments length by one at the end of that length
def getNum(s, n):
	if len(s) == n:
		check(s)
		return
	for i in range(10):
		getNum(s + str(i), n)

# Gets number from getNum, adds the salt value to the end, hashes it, and then checks if the two hashed passwords are the same
def check(s):
	text = open("password_file.txt", "r")
	read = text.readlines()
	for line in read:
		parts = line.split(",")
		user = parts[0]
		salt = parts[1]
		old = parts[2].replace('\n','')
		new = hash_with_sha256(s + salt)
		if(old == new):
			print("The password for", user, "is", s)
			return
	text.close()

def main():
	hex_dig = hash_with_sha256('This is how you hash a string with sha256')
	print(hex_dig)
	for n in range(3,8):
		getNum("",n)
main()
