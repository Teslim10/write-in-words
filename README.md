# write-in-words
writing figures in words
#Create a figure-to-word program, that receives a positive integer as an input, and prints the integer in words.
The program for example takes 90678008 and prints "Ninety million, six hundred and seventy-eight thousand and eight" as result.
Upon doing this, the program asks if the user wants to convert another number. If yes, the program starts all over.
Remember to handle all possible exceptions at the point of receiving user's inputs.
For a pretty output, you are required to first do a study on how figures are really written out in English language, taking note of punctuations etc.
#code to convert figures to word
ones = ('Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine')

twos = ('Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen', 'Seventeen', 'Eighteen', 'Nineteen')

tens = ('Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety', 'Hundred')

suffixes = ('', 'Thousand', 'Million', 'Billion')


def process(number, index, ln):
    print(">>", ln)
    if number == '0':
        return 'Zero'

    length = len(number)

    if (length > 3):
        return False

    number = number.zfill(3)
    words = ''

    hdigit = int(number[0])
    tdigit = int(number[1])
    odigit = int(number[2])

    words += '' if number[0] == '0' else ones[hdigit]
    words += ' Hundred ' if not words == '' else ''

    if index == 0 and ln > 3:
        words += ' and '
    elif words == '':
        words += ''
    elif index == 0 and tdigit == 0 and odigit == 0:
        words += ''
    elif index == 0:
        words += ' and '
    else:
        words += ''

    if (tdigit > 1):
        words += tens[tdigit - 2]
        words += ' '
        words += ones[odigit]

    elif (tdigit == 1):
        words += twos[(int(tdigit + odigit) % 10) - 1]
    elif (tdigit == 0):
        words += ones[odigit]
    if (words.endswith('Zero')):
        words = words[:-len('Zero')]
    else:
        words += ' '

    if (not len(words) == 0):
        words += suffixes[index]

    return words;


def getWords(number):
    length = len(str(number))

    if length > 12:
        return 'This program supports upto 12 digit numbers.'

    count = length // 3 if length % 3 == 0 else length // 3 + 1
    copy = count
    words = []

    for i in range(length - 1, -1, -3):
        words.append(process(str(number)[0 if i - 2 < 0 else i - 2: i + 1], copy - count, length))
        count -= 1;

    final_words = ''
    for s in reversed(words):
        temp = s + ' '
        final_words += temp

    return final_words


# Reading number from user
number = int(input('Enter any number: '))
print('%d in words is: %s' % (number, getWords(number)))
