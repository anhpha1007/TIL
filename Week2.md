```c
//1. scrabble
  // Mảng lưu điểm tương ứng từ A-Z
  int POINTS[] = {1, 3, 3, 2, 1, 4, 2, 4, 1, 8, 5, 1, 3, 1, 1, 3, 10, 1, 1, 1, 1, 4, 4, 8, 4, 10};
  
  
  for (int i = 0, n = strlen(word); i < n; i++)
  
    {
        // Kiểm tra nếu là chữ cái
        if (isupper(word[i]))
        {
            // Chữ hoa: lấy ký tự trừ đi 'A' để ra chỉ số trong mảng POINTS
            score += POINTS[word[i] - 'A'];
        }
        else if (islower(word[i]))
        {
            // Chữ thường: trừ đi 'a'
            score += POINTS[word[i] - 'a'];
        }
        // Nếu không phải chữ cái (dấu câu, số) -> cộng 0 (không cần viết)
    }

//2. caesar

    if (argc != 2)
    {
        printf("Usage: ./caesar key\n");
        return 1;
    }
    //Make sure every character in argv[] is a digit
    
    if(!only_digits(argv[1]))
    {
        printf("Usage: ./caesar key\n");
        return 1;
    }

char rotate(char c, int n)
{
    if (isupper(c))
    {
        // Preserve uppercase letters: shift to 0-25 range, rotate, wrap around, shift back
        return(c - 'A' + n) % 26 + 'A';
    }
    else if (islower(c))
    {
        return(c - 'a' + n) % 26 + 'a';
    }
    return c;
}

//3. substitution
for (int k = 0; k < n; k++)
        {
            if (i != k && tolower(argv[1][i]) == tolower(argv[1][k]))
            {
                printf("Key must not contain duplicate characters.\n");
                return 1;
            }
        }

void substitute_cipher(string plaintext, string key)
{
    for (int t = 0, n = strlen(plaintext); t < n; t++)
    {
        if (isupper(plaintext[t]))
        {
            // Find index 0-25 for uppercase letters
            int index = plaintext[t] - 'A';
            printf("%c", toupper(key[index]));
        }
        else if (islower(plaintext[t]))
        {
            int index = plaintext[t] -'a';
            printf("%c", tolower(key[index]));
        }






















