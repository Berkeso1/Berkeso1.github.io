---
layout: post
title: Digimon Lab
comments: true
mathjax: true

---

# Introducing The CSV

I downloaded the digimon.csv file which contains various digimon and their different attributes.

Here is a an example of what the csv looks like:

| Number | Digimon | Stage | Type  | Attribute | Memory | Equip Slots | HP  | SP  | Atk | Def | Int | Spd |
|--------|---------|-------|-------|-----------|--------|--------------|-----|-----|-----|-----|-----|-----|
| 1      | Kuramon | Baby  | Free  | Neutral   | 2      | 0            | 590 | 77  | 79  | 69  | 68  | 95  |
| 2      | Pabumon | Baby  | Free  | Neutral   | 2      | 0            | 950 | 62  | 76  | 76  | 69  | 68  |
| 3      | Punimon | Baby  | Free  | Neutral   | 2      | 0            | 870 | 50  | 97  | 87  | 50  | 75  |

This csv file gives you every single specific of each digimon which is really cool!

# Average HP of All Digimon

My first task during this assignment was to find the average HP of all the digimon in this file. To do this
I would just need to take the <code style="color: red;">HP</code> column for all rows, sum them up, and divide by the # of values I have.

That was my pseudo code for this problem, but now I will explain what this would look like in code.


    def average_hp():
      with open("digimon.csv", "r") as f:
          data = csv.DictReader(f)
        
          hp_list = [] 

          for row in data:
              health = row.get('HP')

              if health:
                  health = float(health)
                  hp_list.append(health)

      average_hp = sum(hp_list)/len(hp_list)

      return average_hp

So to begin with you always have to open and read the csv using a with statement, which will keep the file open throughout your processes.
Next, in order to track all the <code style="color: red;">HP</code> values in each row, I created a list for all the <code style="color: red;">HP</code> values named <code style="color: red;">hp_list</code>. Utilizing a list here will allow us to use functions like <code style="color: red;">sum()</code> or <code style="color: red;">len()</code> which will make our lives a lot easier. 

Now in order to add all of these <code style="color: red;">HP</code> values to a list I need to run a for loop which goes through all the rows
in the csv. This line of code,<code style="color: red;">health = row.get('HP')</code>, will basicly set the variable <code style="color: red;">health</code> equal to the HP value in a row. Next we will utilize an if statement to set the health value type to a float, because when you take a value from a csv it is stored as a string, meaning you cannot perform mathematical operations on it. That would be a problem. Finally we will append it to the <code style="color: red;">hp_list</code>.

This process will repeat itself for each row of the csv until it reaches the end of it.

Now for the final steps. Because we are using a list, we can utilize the <code style="color: red;">sum()</code> and <code style="color: red;">len()</code> to get our <code style="color: red;">average_hp</code>. To do this we will take the sum of all values in our <code style="color: red;">hp_list</code> and divide the sum by the length of that <code style="color: red;">hp_list</code>.

After completing this proccess we should get an answer of <code style="color: red;">1210.8835341365461</code>, the average hp of all digimon.

### Did Anything Go Wrong?

I mean nothing really went wrong on this question. It was a very straight forward mathematical operation, finding the average of something. However I learned a couple of useful methods which ultimately helped me out a lot. Utilizing a list can be very useful. Because I used a list for this problem I was able to utilize the <code style="color: red;">sum()</code> and <code style="color: red;">len()</code> functions a huge shortcut so that I dont have to use a for loop that cycles through each value and adds them to a variable. Big headache.


# Counting The Number of Digimon With a Specific Attribute

This problem essentially meant that I had have to recreate what the pandas module does, which is make your life easier. My initial approach to this problem was to create a function that will go through all the rows and filter out the attributes (i.e. Number, Digimon, Type, etc) I am looking for. BUT, I forgot that question was asking for a specific attribute within that attribute. These were my initial parameters for the function: 

    def count_digimon(attribute):

This makes absolutely no sense for this problem as all the digimon have this column, there is nothing specific here. Therefore I added a specific attribute to my input parameters for this function so that we can look for specific things under a column. 

    def count_digimon(attribute, specific_attribute):

Thats a lot better!

After fixing that initial mistake, I modified my pseudo code to be clearer: go through all the rows, check if the attribute matches the specific value I’m looking for, and keep a running count. So, something like:

1.  Go through each row.
2.  Look at the attribute I'm interested in (like the "Type").
3.  If the value matches what I’m looking for (e.g., "Vaccine"), increase the count.

Here's how my final code looked:

        def count_digimon(attribute, specific_attribute):
        with open("digimon.csv", "r") as f:
            data = csv.DictReader(f)

            count = 0

            for row in data:
                attribute_row = row.get(attribute)
                
                if attribute_row == specific_attribute:
                    count = count + 1
            return count

First things first, we start by opening the CSV file just like we did in the previous problem. We’re using the <code style="color: red;">csv.DictReader()</code> method again because it lets us access each row in the CSV as a dictionary, where the keys are the column names. This is super handy because we can look up the values in any row just by using the column headers.

Next, we create a <code style="color: red;">count</code> variable and set it to <code style="color: red;">0</code>. We need this to keep track of how many times the specific attribute we’re looking for appears in the CSV:

     count = 0

### Looping Through the Data

    for row in data:
        attribute_row = row.get(attribute)

Here’s where the magic happens. We run a <code style="color: red;">for</code> loop that goes through each row of the CSV file. Inside the loop, we use <code style="color: red;">row.get(attribute)</code> to grab the value from the column we’re interested in (like "Type" or "Stage"). The <code style="color: red;">attribute</code> is just a placeholder for whatever column name we pass into the function.

### Filtering for Specific Attributes

    if attribute_row == specific_attribute:
            count = count + 1

Now we use an <code style="color: red;">if</code> statement to check whether the value we pulled from the row matches the specific attribute we’re looking for. For example, let’s say the attribute we’re searching is "Type," and the specific attribute we want to count is "Vaccine." If the current row’s "Type" value is "Vaccine," we add <code style="color: red;">1</code> to our <code style="color: red;">count</code>.

We repeat this process for every row in the CSV. So, each time the specific attribute appears (e.g., every time we find a "Vaccine" Digimon), we bump up our <code style="color: red;">count</code> by one.

Finally we can return our <code style="color: red;">count</code> variable which holds the information we need to complete this question.

### Did Anything Go Wrong?

At first some things went wrong. As I explained earlier, I misread the question and ended up not accounting for a specific attribute which is the point of this question. However after understanding my error and readjusting my pseudo code I was able to come up with a successful function that does exactly what I want.

# Finding a Valid Digimon Team

This problem was a little more involved compared to the earlier ones. The task was to find all possible combinations of 3 Digimon and filter out the teams that fit specific criteria: a total memory less than 15 and a total attack greater than 300. Sounds straightforward, right? Well, I did run into a couple of bumps along the way, especially with figuring out how to generate all the combinations, but we’ll get to that in a sec.

Here’s the breakdown of the code:

    def digimon_team():
        
    digimon_list = []
    
    valid_digimon = []

To start, I created two lists: one to store all the Digimon and their stats (<code style="color: red;">digimon_list</code>), and another to store only the valid Digimon teams that meet the memory and attack requirements (<code style="color: red;">valid_digimon</code>).

### Reading and Storing the Digimon Data

    with open("digimon.csv", "r") as f:
        data = csv.DictReader(f)
        for row in data:
             name = row.get('Digimon')
             memory = int(row.get('Memory'))
             attack = int(row.get('Atk'))
             
             digimon_list.append({'name': name, 'memory': memory, 'attack': attack})

The next step was pretty boring. Open the CSV, read each row, and grab the name, memory, and attack values for each Digimon. I stored each Digimon’s data as a dictionary ({'name': name, 'memory': memory, 'attack': attack}) inside the digimon_list. This structure gives us a nested list, meaning each entry in the list is a dictionary with the stats of a single Digimon.

At first, I thought I might have to use nested <code style="color: red;">for</code> loops to check for all combinations of Digimon, but that would be inefficient in terms of lines of code, and I like using less lines. So I did some research online and came across the itertools module which contains a combinations function. This is not cheating however as it IS a part of the python standard library.

    all_combinations = combinations(digimon_list, 3)

This single line of code generates all possible combinations of 3 Digimon from my list. Huge relief!

### Checking Each Team's Memory and Attack

        for valid_team in all_combinations:
        total_memory = sum(digimon['memory'] for digimon in valid_team)
        total_attack = sum(digimon['attack'] for digimon in valid_team)
        
        if total_memory < 15 and total_attack > 300:
            
            valid_digimon.append({'team': [digimon['name'] for digimon in valid_team], 'total_memory': total_memory,
                                  'total_attack': total_attack})

Once we have all the combinations of 3 Digimon, we need to check whether they fit the memory and attack requirements. For each valid team of 3 Digimon, I calculate their total memory and total attack by summing up the memory and attack stats of the Digimon in the group.

    total_attack = sum(digimon['attack'] for digimon in valid_team)

This snippet basicly utilizes a <code style="color: red;">for</code> loop to go through each attack key in the dictionary and sum them up. I used this same logic for the <code style="color: red;">total_memory</code> as well.

Then, I used an if statement to filter out teams where:

1. Total memory is less than 15.
2. Total attack is greater than 300.

If a team meets these conditions, I add it to the valid_digimon list as a dictionary. Each entry contains the team members’ names, total memory, and total attack. Here, I’m essentially building a nested list of valid teams, where each team is a dictionary containing another list of Digimon names.

And finally we just return a single team from the <code style="color: red;">valid_team</code> list!

### Did Anything Go Wrong?

The hardest part of this question was figuring out how to generate all the combinations of 3 Digimon without brute forcing it. My initial pseudo code was “loop through the list of Digimon and find every possible group of 3,” but I quickly realized that was going to be super annoying. However as I explained before, I found the <code style="color: red;">itertools.combinations() </code>function, which saved me a lot of time.

Also, nested lists and dictionaries can be pretty tricky, since this is my first time using them. At first, I was confused about how to store each Digimon’s stats, but I figured out that storing them as dictionaries inside a list would let me easily access the memory and attack stats when needed. This ultimately made it easier to filter the teams later.

# Conclusion

During this lab I learned a lot about using lists and dictionaries to make my code more efficient. By using lists and dictionaries, I was able to utilize functions such as <code style="color: red;">sum()</code> or <code style="color: red;">len()</code> which make for a cleaner and better code rather than using a bunch of lines to complete a simple mathematical operation. Furthermore, this lab helped me learn how to manipulate a CSV without the use of pandas, which was really cool. I definitely think I can replace the combinations function from Itertools with my own function. It would make my code more original. Additionally, I believe there is definitely a more efficient way to look for valid digimon teams rather than finding all combinations then filtering. I could maybe... I think I have to think about this a little more, because I have an idea in my head, but I dont know how to put it in words. That would be my next step to improving this code. 
