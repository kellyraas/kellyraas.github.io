Monty Hall Problem
================
Kelly Raas

Many might know the Monty Hall Problem from the [Movie "21"](https://www.youtube.com/watch?v=Zr_xWfThjJ0). For those who are not familiar with it, the setting is as follows:

You are a contestant on a gameshow. The host gives you the option of selecting one from three available doors. Behind one door is a new car, behind the other two are goats. You select one door at random. The host then reveals one of the remaining doors as a Goat Door. Now you have the choice to either stay with your initial choice or switch to the other remaining closed door. The question is: Do you get any advantage when swithcing your choice? Intuitivly, it seems logical that now you have a 50/50 chance that behind the door you chose is the car, and you wouldn't gain anything by switching doors.

However, [Marilyn vos Savant's](https://en.wikipedia.org/wiki/Marilyn_vos_Savant) claimed that under the standard assumptions, contestants who would switch the door had a 2/3 chance of winning the car, while contestants who would stick to their initial choice had only a 1/3 chance. Therefore, her response was that the contestant should switch to the other door.

I could not really make up with this logic and was in doubt whether this was true. So I decided to quickly run a simulation.

This is wat it looks like:

``` r
n = 100000 # set how often to run the experiment
count.choice = 0 
count.switch = 0

for (i in 1:n) {
  
  doors = c(1,2,3) # define the 3 doors
  car = sample(doors)[1] # set door with car prize at random
  choice = sample(doors,1) # choose one door at random
  open.door = doors[which(doors != choice & doors != car)][1] # open one of the two remianing doors (can not be the one with car prize)
  
  switch = doors[which(doors != choice & doors != open.door)] # possible door to switch
  
  if (choice == car) {
    count.choice = count.choice + 1} # sum one for every time you win the car staying with first choice
  else if  (switch == car) {
    count.switch = count.switch + 1} # sum one for every time you win the car when switching door
}

# calculate respective ratios
ratio.win.stay = round(count.choice/n*100,1)
ratio.win.switch = round(count.switch/n*100,1)

count.choice/n*100
```

    ## [1] 33.318

``` r
count.switch/n*100
```

    ## [1] 66.682

So, let's have a look at the results.

``` r
cat("Winning ratio when staying with the initial door:", paste(ratio.win.stay), "%","\n","Winning ratio when switching door:", paste(ratio.win.switch), "%")
```

    ## Winning ratio when staying with the initial door: 33.3 % 
    ##  Winning ratio when switching door: 66.7 %

So, indeed Vos Savant's argument holds true, although it seems totally counterintuitive. Find out more about this Paradox [here](https://en.wikipedia.org/wiki/Monty_Hall_problem).