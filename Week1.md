1. Knowledge
- hello.c => get_string -> hello you
- compare.c => if (x<y), else if, else, ==
- agree.c => get_char, ||
- loops and meow.c
 + while, i++
 + for(int i = 0; i < 3, i++)
 + continue; break; 
 + do … while; 
- create your own function: void meow(void)
- operators: mathematical operations => double it give to the next person

2. Problem set 1
```c
//2.1. mario
 for (int i = 0; i<n; i++)
    {
        for (int k = 0; k < n - 1 - i; k++) // cái này là in a line
        {
            printf(" ");
        }
        for (int m = 0; m < i + 1; m++)
        {
            printf("#");
        }

//2.2. cash

int caculate_quarters(int cents)
{
    int quarters = 0;
    while (cents >= 25)
    {
        quarters++;
        cents = cents - 25;
    }
    return quarters;
}
//or
int caculate_quarters(int cents)
{
    return cents/25;
}
int quarters = caculate_quarters(cents);
    cents = cents - (quarters * 25);

//2.3. credit

int get_checksum(long number)
{
    int sum = 0;
    for (int i = 0; number > 0; i++, number /= 10) // number lần lượt chia cho 10, i tăng dần => số thứ 1 từ dưới lên tương ứng i == 1, ...
    {
        int digit = number % 10;

        if (i % 2 == 0)
        {
            // Add digits in even positions (starting from last)
            sum += digit;
        }
        else
        {
            // Multiply digits in odd positions by 2 and add their digits
            int product = digit * 2;
            sum += (product / 10) + (product % 10);
        }
    }
    return sum;
}
