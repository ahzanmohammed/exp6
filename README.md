import socket

slang = {
    "brb": "be right back",
    "idk": "I don't know",
    "lol": "laughing out loud",
    "tbh": "to be honest",
    "omg": "oh my god"
}

def translate(sentence):
    words = sentence.split()
    result = " ".join(
        slang.get(word.lower(), word)
        for word in words
    )
    return result

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
s.bind(("0.0.0.0", 8080))

print("UDP Translation Server Running...")

while True:
    data, addr = s.recvfrom(4096)
    msg = data.decode()

    translated = translate(msg)

    s.sendto(translated.encode(), addr)



import socket

s = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)

server_address = ("127.0.0.1", 8080)

msg = input("Enter a message: ")

s.sendto(msg.encode(), server_address)

data, addr = s.recvfrom(4096)

print("Translated Message:", data.decode())

s.close()





