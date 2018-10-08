
```flow
st=>start: Good {time_of_day}.
e=>end
op=>operation: Natasha's birthday is coming up. Do you want to send her a gift?
cond=>condition: Yes or No?
cond2=>condition: user suggests or accio suggests?
cond3=>condition: awesome, are you sure you want to proceed with the first choice?
op1=>operation: What would you like to send? 
op2=>operation: Okay, no issues! In case you change your mind, I will be ready to help
op3=>operation: Accio flowers and wine
op4=>operation: sounds good! do you have a budget in mind?
op5=>operation: user suggests
op6=>operation: accio suggests
op7=>operation: do you have any recommendation?
op8=>operation: so what does Natasha like? what are her hobbies?
op9=>operation: I think she loves to play basketball, she is also a very big harry potter fan
op10=>operation: around $30
op11=>operation: actually I will send her a gift, show me some options
op12=>operation: okay, pulling up some results for you!
op13=>operation: accio pulls up results and shows as cards 
with description and prices
op14=>operation: user chooses one gift suggestion
op15=>operation: proceed to checkout
op16=>operation: No, I would like to pick something else
para=>parallel: can you suggest something

st->op->cond->
cond(yes)->op1->cond2->
cond2(yes)->op5->op3->op4->op10->op12->op13->op14->cond3->
cond3(yes)->op15->e
cond3(no)->op16->op12
cond2(no)->op6->op7->op8->op9->op4
cond(no)->op2->op11->cond2
```