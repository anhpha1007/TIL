```c
// 1. volume
// TODO: Copy header from input file to output file
    uint8_t header[HEADER_SIZE];
    fread(header, HEADER_SIZE, 1, input);
//where to store, the size of 1 item in bytes, the quantity of items to read, the source FILE * pointer opened previously with fopen
    fwrite(header, HEADER_SIZE, 1, output);
// fread nguoc lai voi fwrite

// 2. filter
void reflect(int height, int width, RGBTRIPLE image[height][width])
{
     for (int i = 0; i < height; i++)
    {
        for (int j = 0; j < width / 2; j++)
        {
            RGBTRIPLE temp = image[i][j];
            image[i][j] = image[i][width - 1 - j];
            image[i][width - 1 - j] = temp;
        }
    }
    return;
}

if (neighborI >= 0 && neighborI < height && neighborJ >= 0 && neighborJ < width)
{
    totalRed += copy[neighborI][neighborJ].rgbtRed;
    totalGreen += copy[neighborI][neighborJ].rgbtGreen;
    totalBlue += copy[neighborI][neighborJ].rgbtBlue;
    counter++;
}

// 3. recover
while(fread(buffer, 1, BYTES, card) == BYTES)
    {
        // Check if it's a JPEG file
        if (buffer[0] == 0xff && buffer[1] == 0xd8 && buffer[2] == 0xff && (buffer[3] & 0xf0) == 0xe0)
        {
            // If it has already been opened, close it
            if (img != NULL)
            {
                fclose(img);
            }

            // Create filename & it's number
            sprintf(filename, "%03i.jpg", counter);
            img = fopen(filename, "w");
            counter++;
        }

        //Write to that file
        if (img != NULL)
        {
            fwrite(buffer, 1, BYTES, img);
        }
    } 

