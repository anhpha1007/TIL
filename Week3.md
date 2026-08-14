```c
//1. plurality
if (strcmp(name , candidates[m].name) == 0)
        {
            candidates[m].votes++;
            return true;
        }

//2. runoff
typedef struct
{
    string name;
    int votes;
    bool eliminated;
} candidate;

// Record preference if vote is valid
bool vote(int voter, int rank, string name)
{
    for (int i = 0; i < candidate_count; i++)
    {
        if (strcmp(name , candidates[i].name) == 0)
        {
            preferences[voter][rank] = i;
            return true;
        }
    }
    return false;

// Return the minimum number of votes any remaining candidate has
int find_min(void)
{
    int least_vote = voter_count;
    for (int i = 0; i < candidate_count; i++)
    {
        if (!candidates[i].eliminated)
        {
            if (candidates[i].votes < least_vote)
            {
            least_vote = candidates[i].votes;
            }
        }
    }
    return least_vote;
}

// Return true if the election is tied between all candidates, false otherwise
bool is_tie(int min)
{
    int active_candidates = 0;
    int min_candidates = 0;
    for (int i = 0; i < candidate_count; i++)
    {
        if (!candidates[i].eliminated)
        {
            active_candidates++;
            if (candidates[i].votes == min)
            {
                min_candidates++;
            }
        }
    }
    if (min_candidates == active_candidates)
        {
            return true;
        }
    return false;
}

//3. tideman
The Complete Flow Summary
[Voter inputs names] 
       ↓
`vote()` updates ranks[] array
       ↓
`record_preferences()` adds points to 2D matrix preferences[i][j]
       ↓
`add_pairs()` finds all winners where preferences[i][j] > preferences[j][i]
       ↓
`sort_pairs()` ranks pairs from largest margin to smallest
       ↓
`lock_pairs()` locks arrows into locked[i][j] grid (skipping cycles via creates_cycle)
       ↓
`print_winner()` finds candidate with 0 incoming arrows and prints their name!

#include <cs50.h>
#include <stdio.h>
#include <string.h>

// Max number of candidates
#define MAX 9

// preferences[i][j] is number of voters who prefer i over j
int preferences[MAX][MAX];

// locked[i][j] means i is locked in over j
bool locked[MAX][MAX];

// Each pair has a winner, loser
typedef struct
{
    int winner;
    int loser;
} pair;

// Array of candidates
string candidates[MAX];
pair pairs[MAX * (MAX - 1) / 2];

int pair_count;
int candidate_count;
int voter_count;

// Function prototypes
bool vote(int rank, string name, int ranks[]);
void record_preferences(int ranks[]);
void add_pairs(void);
void sort_pairs(void);
void lock_pairs(void);
void print_winner(void);

int main(int argc, string argv[])
{
    // Check for invalid usage
    if (argc < 2)
    {
        printf("Usage: tideman [candidate ...]\n");
        return 1;
    }

    // Populate array of candidates
    candidate_count = argc - 1;
    if (candidate_count > MAX)
    {
        printf("Maximum number of candidates is %i\n", MAX);
        return 2;
    }
    for (int i = 0; i < candidate_count; i++)
    {
        candidates[i] = argv[i + 1];
    }

    // Clear graph of locked in pairs
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = 0; j < candidate_count; j++)
        {
            locked[i][j] = false;
        }
    }

    pair_count = 0;
    voter_count = get_int("Number of voters: ");

    // Query for votes
    for (int i = 0; i < voter_count; i++)
    {
        // ranks[i] is voter's ith preference
        int ranks[candidate_count];

        // Query for each rank
        for (int j = 0; j < candidate_count; j++)
        {
            string name = get_string("Rank %i: ", j + 1);

            if (!vote(j, name, ranks))
            {
                printf("Invalid vote.\n");
                return 3;
            }
        }

        record_preferences(ranks);

        printf("\n");
    }

    add_pairs();
    sort_pairs();
    lock_pairs();
    print_winner();
    return 0;
}

// Update ranks given a new vote
bool vote(int rank, string name, int ranks[])
{
    // FIXED: Loop over candidate_count instead of voter_count
    for (int i = 0; i < candidate_count; i++)
    {
        // FIXED: Compare directly against candidates[i] (not candidates[i].name)
        if (strcmp(name, candidates[i]) == 0)
        {
            ranks[rank] = i;
            return true;
        }
    }
    return false;
}

// Update preferences given one voter's ranks
void record_preferences(int ranks[])
{
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = i + 1; j < candidate_count; j++)
        {
            preferences[ranks[i]][ranks[j]]++;
        }
    }
    return;
}

// Record pairs of candidates where one is preferred over the other
void add_pairs(void)
{
    pair_count = 0;
    for (int i = 0; i < candidate_count; i++)
    {
        for (int j = i + 1; j < candidate_count; j++)
        {
            if (preferences[i][j] > preferences[j][i])
            {
                pairs[pair_count].winner = i;
                pairs[pair_count].loser = j;
                pair_count++;
            }
            else if (preferences[j][i] > preferences[i][j])
            {
                pairs[pair_count].winner = j;
                pairs[pair_count].loser = i;
                pair_count++;
            }
        }
    }
    return;
}

// Sort pairs in decreasing order by strength of victory
void sort_pairs(void)
{
    for (int i = 0; i < pair_count - 1; i++)
    {
        // FIXED: Use pair_count - i - 1 instead of candidate_count - i - 1
        for (int j = 0; j < pair_count - i - 1; j++)
        {
            int strength_j = preferences[pairs[j].winner][pairs[j].loser];
            int strength_j_next = preferences[pairs[j + 1].winner][pairs[j + 1].loser];
            if (strength_j < strength_j_next)
            {
                pair temp = pairs[j];
                pairs[j] = pairs[j + 1];
                pairs[j + 1] = temp;
            }
        }
    }
    return;
}

// Helper function to check if adding locked[winner][loser] creates a cycle
bool creates_cycle(int winner, int loser)
{
    // Base Case: If the path leads back to the original winner, a cycle exists!
    if (loser == winner)
    {
        return true;
    }

    // Check every other candidate to see if 'loser' has an outgoing edge to them
    for (int i = 0; i < candidate_count; i++)
    {
        if (locked[loser][i])
        {
            // Recursively check if 'i' can reach 'winner'
            if (creates_cycle(winner, i))
            {
                return true;
            }
        }
    }

    // No path back to winner was found
    return false;
}

// Lock pairs into the candidate graph in order, without creating cycles
void lock_pairs(void)
{
    for (int i = 0; i < pair_count; i++)
    {
        // Only lock the pair if it does NOT create a cycle
        if (!creates_cycle(pairs[i].winner, pairs[i].loser))
        {
            locked[pairs[i].winner][pairs[i].loser] = true;
        }
    }
    return;
}

// Print the winner of the election
void print_winner(void)
{
    for (int i = 0; i < candidate_count; i++)
    {
        bool has_incoming_edge = false;

        for (int j = 0; j < candidate_count; j++)
        {
            // If someone points to candidate i, i is not the source
            if (locked[j][i])
            {
                has_incoming_edge = true;
                break;
            }
        }

        // If no one points to candidate i, i is the winner
        if (!has_incoming_edge)
        {
            printf("%s\n", candidates[i]);
            return;
        }
    }
    return;
}
