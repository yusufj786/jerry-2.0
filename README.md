# jerry-2.0
intent('Hello world', p => {
    p.play('Hi there');
});
intent(
    'Who\'s there',
    'What\'s your name',
    'who are you',
    p => {
        p.play(
            'My name is Jerry.',
            'It\'s Jerry.',
        );
    },
);

const intentPatterns = [
    'What is your favorite food',
    'What food do you like',
];

intent(intentPatterns, p => {
    p.play('CPU time, yammy!');
});

intent('(I will have|Get me) a coffee, please', p => {
    p.play('Sorry, I don\'t have hands to brew it.');
});
intent('(Start|begin|take|) survey', p => {
    p.play('(Sure.|OK.|) Starting a customer survey.');
});
intent('Let\'s play hide and seek', p => {
    p.play('Sure.');
    p.play('I\'ll count.');
    p.play('One');
    p.play('Two');
    p.play('Three');
    p.play('Found you!');
});

intent('(I want|get me|add) a $(ITEM notebook|cellphone)', p => {
    p.play('Your order is: $(ITEM). It will be delivered within the next 30 minutes.');
});

intent('I want my walls to be $(COLOR green|blue|orange|yellow|white)', p => {
    p.play(`Mmm, ${p.COLOR.value}. Nice, love it!`);
});
intent('What is $(DATE)', p => {
    const formattedDate = p.DATE.moment.format('dddd, MMMM Do YYYY');

    p.play(`${p.DATE.value} is a date`);
    p.play(`It is ${formattedDate}`);
});

intent('Add $(NUMBER) $(INSTRUMENT trumpet_|guitar_|violin_) and $(NUMBER) $(INSTRUMENT trumpet_|guitar_|violin_)', p => {
    console.log('Numbers array:', p.NUMBER_);
    console.log('Instruments array:', p.INSTRUMENT_);
    p.play(`The first position of your order is: ${p.NUMBER_[0].number} ${p.INSTRUMENT_[0].value}`);
    p.play(`The second position of your order is: ${p.NUMBER_[1].number} ${p.INSTRUMENT_[1].value}`);
});

const openContext = context(() => {
    intent('Activate the context', p => {
        p.play('The context is now active');
    });

    follow('Is the context active', p => {
        p.play('Yes. (It is active.|)');
    });
});

let chooseDrink = context(() => {
    follow('(I want|get me) a $(DRINK tea|cup of tea|soda)', p => {
        p.play(`You have ordered a ${p.DRINK.value}.`);
    })
});

intent('Can I have something to drink', p => {
    p.play('(Sure|Yes), we have tea and soda.');
    p.play('Which would you like?');
    p.then(chooseDrink);
});

let confirmOrder = context(() => {
    follow('Yes', p => {
        p.play('Your order is confirmed');
    });
    
    follow('No', p => {
        p.play('Your order is cancelled');
    });
});

let chooseDish = context(() => {
    follow('Get me a $(DISH pizza|burger)', p => {
        p.play(`You have ordered a ${p.DISH.value}. Do you confirm?`);
        p.then(confirmOrder);
    })
});

intent('What is on the menu', p => {
    p.play('We have pizza and burgers');
    p.then(chooseDish);
});

question(
    'What does this (app|script|project) do',
    'What is this (app|script|project|)',
    'Why do I need this',
    reply('This is a Hello World Example project. Its main purpose is to get you introduced to basics of the Alan Platform!'),
);

question(
    'How does this work',
    'How to use this',
    'What can I do here',
    'What (should I|can I|to) say',
    'What commands are available',
    reply('Just say: (hello world|what is the weather today|what is tomorrow|Add two guitars and one violin).'),
);

intent('I want to go to $(LOC) on $(DATE)', p => {
    p.play(`Wait a second, I will check available flights on ${p.DATE.value} for you`);
});


intent('Talk to me', p => {
    p.play('Sure, what do you want to talk about?');
});

intent('Talk to me', p => {
    p.play('Sure, what do you want to talk about?',
           'Sorry, I am not in the mood to talk to anyone');
});

intent('Say $(W hello|goodbye)', p => {
    p.play(`${p.W.value}`);
});

intent('Open the menu', p => {
    p.play({command: 'navigate', screen: 'menu'});
    p.play('Opening the menu');
});

intent('Go back', p => {
    p.play({command: 'navigate', screen: 'back'});
    p.play('Going back');
});
intent('who created you',
       'who is your master', p => {
    p.play('i was created by master yusuf jamadar');
});
intent('Open the menu', p => {
    p.play({command: 'navigate', screen: 'menu'});
    p.play('Opening the menu');
});
intent('Open the menu', p => {
    p.play('Opening the menu');
    p.play({command: 'navigate', screen: 'menu'});
});
intent('Set a 1 minute timer', p => {
    p.play({command: 'setTimer'});
    p.play('Sure, 1 minute, starting now',  opts({deactivate:true}));
    setTimeout(() => {
        p.play({command: 'notifyUser', text: 'You are half way there'}, opts({force:true}));
    }, 30000)
    setTimeout(() => {
        p.play({command: 'stopTimer'}, opts({force:true}));
        p.play('Time is up', opts({activate:true, deactivate:true}))
    }, 60000)
})
intent('tell me more about you',
       'can you tell me something about u', 
       'are you an ai',
       'can you tell me about you',
        p => {
    p.play('yes i am an ai i was created by master yusuf jamadar thats all i can tell you about me');
});
intent('What is the weather?', p => {
    p.play('The weather is the day-to-day state of the atmosphere');
});

intent('What is the weather today?', p => {
    p.play('The weather today is great!')
});
question(
    'i love u',
    'do you love me',
    reply('no i am an AI i cant be in love with u because i am an AI.'),
);
intent('i love u',
       'do you love me', p => {
    p.play('no i am an AI i cant be in love with u because i am an AI.');
});
intent('where do you live',
       'where do you stay', p => {
    p.play('i live in cloud storage');
});
intent('add 2+2',
       '2+2', 
       '2+2 solve', p => {
    p.play('2+2 is 4');
});
intent('substract 2-2',
       '2-2', 
       'solve 2-2',
       'remove 2 in 2', p => {
    p.play('2-2 is 0');
});


question('what is this', p =>  {
    p.play('This is an example app with voice capabilities. (Powered by Alan|Voice support is provided by Alan)');
});

question('what is Alan (AI|Platform|)', p => {
    p.play('Alan (AI|Platform) is a platform that will allow you to voice enable any application. Be it mobile app on iOS or Android, or a web page.');
});

question('what (platforms|SDK|frameworks) are supported', p => {
    p.play('Alan (AI|Platform) supports native iOS, Android, and Web applications. As well as Flutter, Ionic and many other popular frameworks.');
});
// {Name: Calculator}

title('Calculator');

function plus(v1, v2) {
    return v1 + v2;
}

function minus(v1, v2) {
    return v1 - v2;
}

function mult(v1, v2) {
    return v1 * v2;
}

function divide(v1, v2) {
    if (v2 === 0) {
        return 'infinity';
    }
    return v1 / v2;
}

function squareRoot(v1) {
    if (v1 < 0) {
        return 'you can\'t take a square root of a negative number';
    }
    return Math.sqrt(v1);
}

function cubicRoot(v1) {
    if (v1 < 0) {
        return 'you can\'t take a cubic root of a negative number';
    }
    return Math.cbrt(v1);
}

function roundToLimit(num) {
    if(Math.abs(num) >= 1e19 || !num.toString().includes('e')) {
        return num;
    }
    const digitsCount = 15 - numDigits(num);
    return +(Math.round(num + 'e+' + digitsCount) + 'e-' + digitsCount);
}

function numDigits(x) {
    return Math.max(Math.floor(Math.log10(Math.abs(x))), 0) + 1;
}

function power(x, n) {
    return Math.pow(x, n);
}

function cube(x) {
    return power(x,3);
}

function square(x) {
    return power(x,2);
}

const operatorMap = {
    'plus': plus,
    'add': plus,
    '+': plus,
    'minus': minus,
    'subtract': minus,
    'take away': minus,
    '-': minus,
    'times': mult,
    'multiply': mult,
    '*': mult,
    'into': mult,
    'cubed': cube,
    'squared': square,
    'to the power': power,
    'power': power,
    'divide': divide,
    'divided': divide,
    'over': divide,
    '/': divide,
    'cubic root': cubicRoot,
    'square root': squareRoot,
    'root': squareRoot,
};

onCreateContext(p => {
    p.state.result = 0;
});

intent(
    '(what is|how much is|calculate|compute|) $(NUMBER) $(OPERATOR *|+|-|/|plus|minus|over|divided|divide|times|to the power) (of|) $(NUMBER)',
    '(what is|how much is|calculate|compute|) $(OPERATOR multiply|divide) $(NUMBER) (by|on|) $(NUMBER)',
    '(what is|how much is|calculate|compute|) $(OPERATOR cubic root|square root|root) of $(NUMBER)',
    '(what is|how much is|calculate|compute|) $(NUMBER) $(OPERATOR cubed|squared)',
    '(what is|how much is|calculate|compute|) $(NUMBER) to the $(ORDINAL) $(OPERATOR power)',
    p => {
        const operator = operatorMap[p.OPERATOR.value];

        if (!operator) {
            p.play(`(Sorry|) I can't do ${p.OPERATOR} (yet|)`);
            return;
        }

        if (!p.NUMBER_.length) {
            p.play('I need at least one argument');
            return;
        }

        if (p.NUMBER_.length === 1) {
            if(p.ORDINAL) {
                p.state.result = operator(p.NUMBER.number, p.ORDINAL.number);
                p.state.result = roundToLimit(p.state.result);
                p.play(
                    `${p.NUMBER.number} to the ${p.ORDINAL.number} power (is|equals to) ${p.state.result}`,
                    `(it's|) ${p.state.result}`,
                );
            } else {
                if ((p.OPERATOR.value === 'square root' || p.OPERATOR.value ==='root') && (p.NUMBER.number < 0)) {
                    p.play(`I can't take a square root of a negative number ${p.NUMBER.number}`);
                    return;
                }

                if ((p.OPERATOR.value === 'cubic root') && (p.NUMBER.number < 0)) {
                    p.play(`I can't take a cubic root of a negative number ${p.NUMBER.number}`);
                    return;
                }

                p.state.result = operator(p.NUMBER.number);
                p.state.result = roundToLimit(p.state.result);
                p.play(
                    `${p.OPERATOR} (of) ${p.NUMBER_[0]} (is|equals to) ${p.state.result}`,
                    `(it's|) ${p.state.result}`,
                );
            }
        }

        if (p.NUMBER_.length === 2) {
            if ((p.OPERATOR.value === 'divide' || p.OPERATOR.value === '/') && (p.NUMBER_[1].number === 0)) {
                p.play(`I can't divide ${p.NUMBER_[0]} by zero`)
            } else {
                p.state.result = operator(p.NUMBER_[0].number, p.NUMBER_[1].number);
                p.state.result = roundToLimit(p.state.result);
                p.play(
                    `${p.NUMBER_[0]} ${p.OPERATOR} ${p.NUMBER_[1]} (is|equals to) ${p.state.result}`,
                    `(it's|) ${p.state.result}`,
                );
            }
        }
    },
);

follow('$(OPERATOR *|+|-|/|plus|minus|over|divided|divide|times) $(NUMBER)', p => {
    const operator = operatorMap[p.OPERATOR.value];
    if (!operator) {
        p.play(`(Sorry|) I can't do ${p.OPERATOR} (yet|)`);
        return;
    }
    const prevState = p.state.result;
    p.state.result = roundToLimit(operator(prevState, p.NUMBER.number));
    p.play(
        `${prevState} ${p.OPERATOR} ${p.NUMBER} (is|equals to) ${p.state.result}`,
        `(it's|) ${p.state.result}`,
    );
});


// Q/A for Alan Playground
intent(
    'What does this app do?',
    'How does this work?',
    'What can I do here?',
    reply('This is a calculator project, and you can do simple math operations here Just ask me any mathematical calculation, and I will try to answer it'),
);
// {Name: Calendar}
// {Description: What day is tomorrow}

title("General calendar")

intent(
    "what (date|day) $(V is|was|will be|would be|) $(DATE) $(T next year|last year|)",
    p => {
        let momentDate;
        if (p.T.value === "last year"){
            momentDate = p.DATE.moment.add(-1, 'Y');
        }
        else if (p.T.value === "next year"){
            momentDate = p.DATE.moment.add(1, 'Y');
        }
        else {
            momentDate = p.DATE.moment;
        }
        let res = momentDate.format("dddd, MMMM Do YYYY");
        p.play(`${p.DATE} ${p.V} ` + res);
    }
);

follow(
    "(and|) (what|) (about|) $(DATE)",
    p => {
        let res = p.DATE.moment.format("dddd, MMMM Do YYYY");
        p.play(`${p.DATE} ` + res)
    }
);

intent(
    "(what is|) is (my|) timezone",
    p => {
        p.play("Your current timezone is " + p.timeZone);
    }
);

intent(
    "(what is|) (the|) (current|) time (now|)",
    p => {
        p.play("Now is " + api.moment().tz(p.timeZone).format("h:mmA"));
    }
);

intent(
    "(what is|) (the|) (current|) (day|date) (now|today|)",
    p => {
        p.play("Now is " + api.moment().tz(p.timeZone).format("dddd, MMMM Do YYYY"));
    }
);

intent(
    "(what is|) (the|) (current|) day and time (now|today|)",
    p => {
        p.play("Now is " + api.moment().tz(p.timeZone).format("dddd, h:mmA"));
    }
);


title("Alan calendar")

intent(
    "when (Alan|) Turing was born",
    p => {
        let turingBirthdate = api.moment("19120612", "YYYYMMDD");
        p.play(`Alan Turing was born ${turingBirthdate.fromNow()} on ${turingBirthdate.format("dddd, MMMM Do YYYY")}`);
    }
);


title("Moon landing calendar")

intent(
    "when was the first (unmanned|) (moon landing|lunar landing)",
    p => {
        let moonLandingDateLuna = api.moment("19590913", "YYYYMMDD");
        p.play(`The first unmanned moon landing was on ${moonLandingDateLuna.format("dddd, MMMM Do YYYY")}, ${moonLandingDateLuna.fromNow()}`);
    }
);

var mannedLanding = p => {
    let moonLandingDateApollo = api.moment("19690720", "YYYYMMDD");
    p.play(`The first manned moon landing was on ${moonLandingDateApollo.format("dddd, MMMM Do YYYY")}, ${moonLandingDateApollo.fromNow()}`);
}

follow("and manned", mannedLanding);

intent("when was the first manned (moon landing|lunar landing)", mannedLanding);

// see https://momentjs.com, moment js library is available through api.moment
// {Name: Directions}
// {Description: Provides navigation and location information. "Take me to my next meeting", "Where is my meeting tomorrow morning?"}

title("Change address.")

intent("(change|update|set) $(L home|office|work) (address|location) to $(LOC)",
    reply("do you want to set $(L) address to $(LOC)",
        follow("(yes|ok|sure)", reply("ok, set")),
        follow("(no|nope|cancel)", reply("cancelled"))))

intent("(remember|set|update) (this|current|that) (location|address|) as $(L home|office|work) (address|)",
    p => {
        p.play("set")
    })


let where = context(()=> {
    title("Question where?")

    follow("(to my|to|my|) $(L home|office|work|gym)",
        async p => p.resolve(await getLocation(p, "your", p.L.value)))

    follow("$(NAME) ('s|) $(L home|office|work)",
        async p => p.resolve(await getLocation(p, p.NAME.value, p.L.value)))

    follow("(to|) $(C next|last|current) $(E meeting|event|appointment)",
        p => p.play(`navigating to ${p.C} ${p.E}`))

    follow("$(LOC)",
        p => p.resolve(p.LOC.value))

    follow('never mind', '(cancel|forget) (that|)',
        p => p.resolve(null))

    fallback(
        'Where should I navigate? It can be home, (office|work), work or a specific address',
        'I can navigate to home, office, (work|gym) or a specific address')
})

let whatAddress = context(() => {
    title("Question what address?")

    onCreateContext(p => {
        p.state = []
    })

    follow("$(NUMBER)",
        p => {
            p.state.push(p.NUMBER.number)
            checkAddress(p)
        })

    follow("(it's|the address is|) $(LOC)",
        p => {
            p.state.push(p.LOC.value)
            checkAddress(p)
        })

    follow('never mind', '(cancel|forget) (that|)',
        p => {
            p.resolve(null)
        })

    fallback('(Please|Just|) tell me the (address|location)',
             'I need the (location|address)')

    function checkAddress(p) {
        let a = parseAddress(p.state)
        if (a.valid) {
            p.resolve(a.address)
        } else {
            //p.onIdle(3000, function() {
              p.play("please tell me a valid address")
            //})
        }
    }
})

function parseAddress(items) {
    let addr = items.join(' ');
    if (addr.length > 5) {
        return {valid: true, address: addr};
    }
    return {valid: false};
}

function getLocation(p, person, loc) {
    let address = null;//''api.getAddress(person, loc)
    if (address) {
        return Promise.resolve(address);
    } else {
        p.play(`what is ${person} ${loc} address?`);
        return p.then(whatAddress);
    }
}


title("Navigation.")

intent("navigate (me|)", "build (me|) (a|) route (for me|)",
    reply("where (to|)?",
        async p => {
            let address = await p.then(where)
            if (address) {
                p.play("navigating to " + address)
            } else {
                p.play('(ok|fine|sure)')
            }
        }))

intent("(navigate me|build route|get me) (to|) $(LOC)",
    p => {
        p.play(`navigating to ${p.LOC}`)
    })

intent("(navigate|take me|get me|build route) (to|) (my|) $(L home|office|work|gym)",
       "(get|take) me (to|) (my|) $(L home)",
    async p => {
        let addr = await getLocation(p, "your", p.L.value)
        if (addr) {
            p.play(`navigating to ${p.L}, ${addr}`)
        } else {
            p.play('(ok|fine|sure)')
        }
    })

// {Name: Food_Ordering}
// {Description: Food Ordering demo app for delivering food}

/*
This is a script for Food Ordering demo app for delivering food
Now there are four categories for food: drinks, pizza, street food, desserts.
*/

const menu = {
    "drink": [
        {id: "sod", title: "Cola", price: 2, type: "drink", alt: ["Coca-cola", "Soda", "Coca cola"]},
        {id: "amr", title: "Americano", price: 1, type: "drink"},
        {id: "lat", title: "Latte", price: 3, type: "drink"},
        {id: "cap", title: "Cappuccino", price: 3, type: "drink"},
        {id: "orj", title: "Orange juice", price: 3, type: "drink"},
        {id: "tea", title: "Tea", price: 3, type: "drink"}
    ],
    "pizza": [
        {id: "prn", title: "Pepperoni", price: 14, type: "pizza", alt: ["Pepperoni pizza"]},
        {id: "mrg", title: "Margarita", price: 10, type: "pizza", alt: ["Margarita pizza"]},
        {id: "4ch", title: "Cheese", price: 10, type: "pizza", alt: ["Cheese pizza"]},
        {id: "haw", title: "Hawaiian", price: 10, type: "pizza", alt: ["Hawaiian pizza"]}
    ],
    "street food": [
        {id: "brt", title: "Burrito", price: 12, type: "street food"},
        {id: "brg", title: "Burger", price: 23, type: "street food"},
        {id: "tco", title: "Taco", price: 10, type: "street food"},
        {id: "snd", title: "Sandwich", price: 10, type: "street food"}
    ],
    "dessert": [
        {id: "apl", title: "Apple pie", price: 5, type: "dessert"},
        {id: "chc", title: "Cheesecake", price: 15, type: "dessert"}
    ]
};

const dishes = [
    "Spaghetti",
    "Bruschetta",
    "Chicken Parmigiana",
    "Panini",
    "Panna Cotta",
    "Tramezzino",
    "Tiramisu",
    "Tortellini",
    "Lasagna",
    "Buffalo Chicken Wings",
    "Tater Tots",
    "Hot Dogs",
    "Barbecue Ribs",
    "Biscuits and Gravy",
    "Meatloaf",
    "Grits",
    "Hamburger",
];


const CATEGORY_ALIASES = _.reduce(Object.keys(menu), (a, p) => {
    const key = p.toLowerCase();
    a[key] = a[key + "s"] = a[key + "es"] = key;
    return a;
}, {});

const ID_TO_TYPES = _.reduce(menu, (a, p) => {
    p.forEach(i => a[i.id] = i.type);
    return a;
}, {});

const ITEM_ALIASES = _.reduce(menu, (a, p) => {
    p.forEach(i => {
        let key = i.title.toLowerCase();
        a[key] = a[key + "s"] = a[key + "es"] = i;
        if (i.alt) {
            i.alt.forEach(s => a[s.toLowerCase()] = a[s.toLowerCase() + "s"] = a[s.toLowerCase() + "es"] = i)
        }
    });
    return a;
}, {});

const ITEMS_INTENT = Object.keys(ITEM_ALIASES).join("|");
const DISHES_INTENT = dishes.join('|');
const CATEGORY_LIST = Object.keys(CATEGORY_ALIASES).join("|");

intent(
    `(Back|go back)`,
    p => {
        let route = p.visual.route ? p.visual.route.toLowerCase() : null;
        switch (route) {
            case "/finish-order":
            case "/cleared-order":
                p.play({command: 'navigation', route: '/menu'});
                break;
            default:
                p.play({command: 'navigation', action: 'back'});
        }
        p.play(`OK`);
    }
);

intent(
    `What is (it|the app|application)`,
    `Where am I`,
    p => {
        p.play("(This is|It's) (just|simple) Food Ordering example application for (food delivery service|pizza ordering).");
    }
);

intent(
    `What (kind|types) of food do you have (to order|)`,
    `What do you have (to order|)`,
    `What (food|) is available`,
    `What can I (order|have|get)`,
    p => {
        p.play(
            "We have several pizzas, street foods, desserts, and drinks available. (What would you like to order?|)",
            "We offer pizzas, street foods, desserts, and drinks. (What would you like to order?|)"
        );
    }
);

intent(
    `What (can|should|must) I (do|say|pronounce)`,
    `Help (me|)`,
    `What to do (here|)`,
    `How to start`,
    p => {
        let route = p.visual.route ? p.visual.route.toLowerCase() : null;
        switch (route) {
            case "/menu/pizza":
            case "/menu/street food":
            case "/menu/dessert":
            case "/menu/drink":
                p.play("Here you can navigate through the menu and add and remove food to your order. To open menu category say (Open|go to) (drinks|pizza|street food|desserts). To add an item to your cart say 'add taco or add (2|3) (burgers|margaritas|latte)'. To remove an item from your cart say 'remove taco or remove (2|3) (burgers|margritas)'. To finish order and checkout say that is all or checkout.");
                break;
            case "/cart":
                p.play("You are in your cart. You should answer questions about delivery address and time. You can change the address by saying 'set address' and you can change delivery time when you say 'set time'.");
                break;
                //TODO: Not returned in VS route
            case "time":
                p.play("Enter or say what time we should deliver an order to you.");
                break;
                //TODO: Not returned in VS route
            case "address":
                p.play(
                    "Here you can point the address for delivering your order.",
                    "Please, enter or say what is the delivery address?"
                );
                break;
            case "/finish-order":
                p.play("You finished your order, if you want to make another order say 'go back' or 'open menu' and add new items to your order.");
                break;
            case "/cleared-order":
                p.play("You have (cleared|canceled) your order, if you want to make another order say 'go back' or 'open menu' and add new items to your order.");
                break;
            default:
                p.play(
                    "We have several pizzas, street foods, desserts, and drinks available.",
                    "We offer pizzas, street foods, desserts, and drinks. What would you like to order?"
                );
        }
    }
);

let getProduct = context(() => {
    intent(`(Add|I want|order|get me|and|) $(ITEM ${ITEMS_INTENT})`, p => {
        return p.resolve(p.ITEM.value);
    });
});

intent(
    `What $(CAT ${CATEGORY_LIST}) do you have?`,
    `(Order|get me|add|) $(NUMBER) $(CAT ${CATEGORY_LIST})`,
    async p => {
        let key = CATEGORY_ALIASES[p.CAT.value.toLowerCase()];
        let value = p.CAT.endsWith('s') ? p.CAT.value : p.CAT.value + "s";
        p.play({command: 'navigation', route: `/menu/${key}`});
        p.play(
            `We have (a few|several) ${value} available:`,
            `You can choose from a few different ${value}:`,
            `There are a few types of ${value} (we have|available):`
        );
        for (let i = 0; i < menu[key].length; i++) {
            p.play({command: 'highlight', id: menu[key][i].id});
            p.play((i === menu[key].length - 1 ? "and " : "") + menu[key][i].title);
        }
        p.play(`Which ${value} would you like?`);
        p.play({command: 'highlight', id: ''});
        if (p.NUMBER) {
            let product = await p.then(getProduct);
            p.play(product);
            let items = [{value: product}];
            addItems(p, items, 0);
        }
    }
);

intent(
    `How to (make an|) order`,
    `Give me an (order|) example`,
    p => {
        p.play("Choose food category and add items from menu to order. For example, you can say: (select pizza, add 3 pepperoni, checkout|open street food, add 5 burgers, if you wish to remove some items say remove one burger, what is my order? checkout|open drinks, add one latte, add one cappuccino, that is all)");
    }
);

intent(`(Open|what do you have in|choose|select|) $(ITEM ${CATEGORY_LIST})`, p => {
    p.play({command: 'navigation', route: `/menu/${CATEGORY_ALIASES[p.ITEM.toLowerCase()]}`});
    p.play(`Opening ${p.ITEM} menu`);
});

intent(`Open cart`, p => {
    p.play({command: 'navigation', route: '/cart'});
    p.play(`Here is your cart`);
});

intent(`Open menu`, p => {
    p.play({command: 'navigation', route: '/menu'});
    p.play(`Look at our menu`);
});

intent(`Scroll down`, p => {
    p.play({command: 'scroll', direction: 'down'});
});

intent(`Scroll up`, p => {
    p.play({command: 'scroll', direction: 'up'});
});

intent(`(Clear|remove|empty|cancel) order`, p => {
    p.play({command: 'clearOrder', route: 'cleared-order'});
    p.play(`Your order has been canceled`);
});

let confirm = context(() => {
    intent(`(Yes|ok|correct|procede|confirm|continue|next|sure|I do|go on) (please|sir|)`, p => {
        p.play("(Great,|) your order has been confirmed. And will be delivered");
        if (p.visual.address) {
            p.play({command: 'highlight', id: 'address'});
            p.play(` to ${p.visual.address}`);
        }
        if (p.visual.date) {
            p.play({command: 'highlight', id: 'date'});
            p.play(` on ${p.visual.date}`);
        }
        if (p.visual.address) {
            p.play({command: 'highlight', id: 'time'});
            p.play(` at ${p.visual.time}`);
        }
        p.play({command: 'finishOrder'});
        p.resolve(null);
    });

    intent(
        `(No|change|invalid|nope|not correct|stop|back)`,
        `(Need|can you|please) (fix|change|update) (delivery|) (address|time|date)`,
        p => {
            p.play({command: 'navigation', route: '/cart'});
            p.play("OK, please (make neccessary corrections|update an order|fix what you want).");
            p.resolve(null);
        }
    );

    fallback("(Sorry,|) I didn't get it. Do you want to confirm your order?");
})

let playDelivery = function (p, address, date, time) {
    if (!address) {
        p.play("What is delivery address?");
    } else if (!time) {
        p.play({command: 'highlight', id: 'time'});
        p.play("What is delivery time?");
    } else if (!date) {
        p.play({command: 'highlight', id: 'date'});
        p.play("What is delivery date?");
    } else {
        p.play({command: 'navigation', route: '/cart'});
        p.play(`OK, your order will be delivered to ${address}. Do you want to confirm your order?`);
        p.then(confirm, {address, date, time});
        return false;
    }
    return true;
}

// request delivery time
let checkout = context(() => {
    intent(`$(LOC)`, p => {
        p.play({command: 'address', address: p.LOC.value});
        p.play({command: 'highlight', id: 'address'});

        let date = api.moment().tz(p.timeZone).format("MMMM Do");
        let time = api.moment().tz(p.timeZone).add(30, 'minutes').format("h:mm a");
        p.play({command: "time", time: time, date: date});
        playDelivery(p, p.LOC.value, date, time);
    });

    intent(
        `$(TIME)`,
        `$(T now|asap|right now|as soon as possible)`,
        `$(DATE)`,
        `$(TIME) $(DATE)`,
        `$(DATE) $(TIME)`,
        p => {
            let time, date;
            if (p.T) {
                // deliver in 30 minutes
                date = api.moment().tz(p.timeZone).format("MMMM Do");
                time = api.moment().tz(p.timeZone).add(30, 'minutes').format("h:mm a");
                p.play({command: 'highlight', id: 'date'});
            }
            if (p.TIME) {
                time = p.TIME.value;
                date = date ? date : p.visual.date;
                p.play({command: 'highlight', id: 'time'});
            }
            if (p.DATE) {
                date = p.DATE.moment.format("MMMM Do");
                time = time ? time : p.visual.time;
                p.play({command: 'highlight', id: 'date'});
            }
            p.play({command: 'time', time: time, date: date});

            playDelivery(p, p.visual.address, date, time);
        }
    );

    intent(`Back (to order|)`, p => {
        p.play({command: 'navigation', route: '/cart'});
        p.play("OK");
        p.resolve(null)
    });
});


let date = context(() => {
    intent(
        `$(TIME)`,
        `$(T now|asap|right now|as soon as possible)`,
        `$(DATE)`,
        `$(TIME) $(DATE)`,
        `$(DATE) $(TIME)`,
        p => {
            let time, date;
            if (p.T) {
                // deliver in 30 minutes
                date = api.moment().tz(p.timeZone).format("MMMM Do");
                time = api.moment().tz(p.timeZone).add(30, 'minutes').format("h:mm a");
                p.play({command: 'highlight', id: 'date'});
            }
            if (p.TIME) {
                time = p.TIME.value;
                date = date ? date : p.visual.date;
                p.play({command: 'highlight', id: 'time'});
            }
            if (p.DATE) {
                date = p.DATE.moment.format("MMMM Do");
                time = time ? time : p.visual.time;
                p.play({command: 'highlight', id: 'date'});
            }
            p.play({command: 'time', time: time, date: date});

            playDelivery(p, p.visual.address, date, time);
        }
    );
});

intent(`(Add|I want|do you have|order) $(F ${DISHES_INTENT})`, p => {
    p.play(`Unfortunately you can't add ${p.F} to your order. But we can offer it in our restaurant.`);
});

// add items to order
intent(
    `(Add|I want|order|get|and|) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(ITEM ${ITEMS_INTENT}) (and|)  $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|)  $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(ITEM ${ITEMS_INTENT}) (and|)  $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|and|) $(ITEM ${ITEMS_INTENT})`,
    p => addItems(p, p.ITEM_, 0)
);


intent(
    `(Add|I want|order|get me|) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    `(Add|I want|order|get me|) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    p => addItems(p, p.ITEM_, 1)
);

intent(
    `(Add|I want|order|get me|) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    p => addItems(p, p.ITEM_, 2)
);

intent(
    `(Add|I want|order|get me|) $(NUMBER) $(ITEM ${ITEMS_INTENT}) (and|) $(ITEM ${ITEMS_INTENT}) (and|) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    p => addItems(p, p.ITEM_, 0, [0, -1, 1])
);

function addItems(p, items, shift, pos = []) {
    let answer = "";
    let id, name;
    for (let i = 0; i < items.length; i++) {
        id = ITEM_ALIASES[items[i].value.toLowerCase()].id;
        name = items[i].value.toLowerCase();
        if (!id) {
            if (!_.isEmpty(answer)) {
                p.play(answer);
            }
            p.play(`(Sorry,|) I can't find ${items[i].value} in the menu.`);
            return;
        } else {
            let number = p.NUMBERs && p.NUMBERs[i - shift] ? p.NUMBERs[i - shift].number : 1;
            if (!_.isEmpty(pos)) {
                number = i < pos.length && pos[i] > -1 ? p.NUMBERs[pos[i]] : 1;
            }
            if (number > 99) {
                p.play(`(Sorry,|) the quantity of ${items[i].value} is too high.`);
                return;
            }
            p.play({command: 'addToCart', item: id, quantity: number});
            answer += i > 0 ? ` and ` : `Added `;
            answer += `${number} ${items[i].value} `;
            if (ID_TO_TYPES[id] === "pizza" && !name.includes("pizza")) {
                answer += number > 1 ? "pizzas " : "pizza ";
            }
        }
    }
    answer += "to your order.";
    p.state.lastId = id;
    p.state.lastName = name;
    p.play({command: 'navigation', route: '/cart'});
    p.play(answer);
}

// replace items
intent(`Change (one of |) the $(ITEM ${ITEMS_INTENT}) (to|by) a $(ITEM ${ITEMS_INTENT})`, p => {
    if (p.ITEM_ && p.ITEM_.length !== 2) {
        p.play("Sorry, you should provide exactly two items in this request.");
        return;
    }
    let delId = ITEM_ALIASES[p.ITEM_[0].value.toLowerCase()].id;
    if (!delId) {
        p.play(`Can't find ${p.ITEM_[0]} in the menu`);
    } else {
        let addId = ITEM_ALIASES[p.ITEM_[1].value.toLowerCase()].id;
        let delName = p.ITEM_[0].value.toLowerCase();
        let addName = p.ITEM_[1].value.toLowerCase();
        if (!addId) {
            p.play(`Can't find ${p.ITEM_[1]} in the menu.`);
        } else {
            p.state.lastId = addId;
            p.state.lastName = addName;
            let delNumber = p.NUMBER_ && p.NUMBER_[0] ? p.NUMBER_[0].number : 1;
            let number_add = p.NUMBER_ && p.NUMBER_[1] ? p.NUMBER_[1].number : 1;
            let postfix_add = "";
            let postfix_del = "";
            if (ID_TO_TYPES[addId] === "pizza" && !addName.includes("pizza")) {
                postfix_add = number_add > 1 ? "pizzas" : "pizza";
            }
            if (ID_TO_TYPES[delId] === "pizza" && !delName.includes("pizza")) {
                postfix_del = delNumber > 1 ? "pizzas" : "pizza";
            }
            let ans = '';
            let order = p.visual.order || {};
            if (!order[delId]) {
                ans = `${p.ITEM_[0]} has not been ordered yet, `;
            } else {
                p.play({command: 'removeFromCart', item: delId, quantity: delNumber});
                ans = `Removed ${delNumber} ${p.ITEM_[0]} ${postfix_del} and `;
            }
            p.play({command: 'addToCart', item: addId, quantity: number_add});
            p.play(ans + ` added ${number_add} ${p.ITEM_[1]} ${postfix_add}.`);
        }
    }
    p.play({command: 'navigation', route: '/cart'});
});

intent(
    `Add (another|) $(NUMBER) more`,
    `Add another`,
    p => {
        if (p.state.lastId) {
            let number = p.NUMBER && p.NUMBER.number > 0 ? p.NUMBER.number : 1;
            if (number > 99) {
                p.play("(Sorry,|) the number is too high.");
                return;
            }
            p.play({command: 'addToCart', item: p.state.lastId, quantity: number});
            p.play(`Added another ${number} ${p.state.lastName}`);
        } else {
            p.play("Sorry, You should order something first.");
        }
    }
);

// remove or update order items
intent(
    `(Remove|delete|exclude) $(ITEM ${ITEMS_INTENT})`,
    `(Remove|delete|exclude) $(NUMBER) $(ITEM ${ITEMS_INTENT})`,
    p => {
        let order = p.visual.order || {};
        let id = ITEM_ALIASES[p.ITEM.value.toLowerCase()].id;
        if (!order[id]) {
            p.play(`${p.ITEM} has not been ordered yet`);
        } else {
            let quantity = order[id] ? order[id].quantity : 0;
            let deteleQnty = p.NUMBER ? p.NUMBER.number : quantity;
            if (quantity - deteleQnty <= 0) {
                p.play('Removed all ' + p.ITEM.value);
            } else {
                p.play(`Updated ${p.ITEM} quantity to ${quantity - deteleQnty}`);
            }
            p.play({command: 'removeFromCart', item: id, quantity: deteleQnty});
            p.play({command: 'navigation', route: '/cart'});
        }
    }
);

// play order details
intent(`(My order|order details|details)`, p => {
    let order = p.visual.order;
    if (_.isEmpty(order)) {
        p.play(
            "You have not ordered anything yet.",
            "Your cart is empty."
        );
        return;
    }
    p.play("You have ordered:");
    for (let product in order) {
        if (order.hasOwnProperty(product)) {
            p.play(" " + order[product].quantity + " " + order[product].title);
        }
    }
});

// set address
intent(
    `(Set|change|replace) (delivery|) address`,
    `(Delivery|) address is (not correct|invalid)`,
    p => {
        if (_.isEmpty(p.visual.order)) {
            p.play("Please, add something to your order first.");
        } else {
            p.play({command: 'highlight', id: 'address'});
            p.play("What is the delivery address?");
            p.then(checkout);
        }
    }
);

const COMPOUND_DELIVERY_INTENT = [
    `Deliver to $(LOC)`,
    `Delivery address (is|) $(LOC)`,
    `Deliver to $(LOC) (at|on|) $(DATE)`,
    `Deliver to $(LOC) (at|on|) $(DATE) (at|on|) $(TIME)`,
    `Deliver (at|on|) $(DATE)`,
    `Delivery date (is|) $(DATE)`,
    `Deliver (at|on|) $(TIME)`,
    `Delivery time (is|) $(TIME)`,
    `Deliver (at|on|) $(DATE) (at|on|) $(TIME)`
]

intent(COMPOUND_DELIVERY_INTENT, p => {
    if (_.isEmpty(p.visual.order) || !p.visual.total) {
        p.play("Your cart is empty, please make an order first.");
        return;
    }
    let address = p.visual.address;
    let date = p.visual.date;
    let time = p.visual.time;

    p.play({command: 'checkout'});

    if (p.LOC) {
        p.play({command: 'address', address: p.LOC.value});
        address = p.LOC.value;
    }
    if (p.DATE || p.TIME) {
        date = p.DATE ? p.DATE.moment.format("MMMM Do") : null;
        time = p.TIME ? p.TIME.value : null;
        p.play({command: 'time', time: time, date: date});
    }
    if (playDelivery(p, address, date, time)) {
        p.then(checkout);
    }
});

// set date/time
intent(
    `(Let's|) (set|choose|select|change) (delivery|) (time|date)`,
    `(Delivery|) (date|time) is (not correct|invalid)`,
    p => {
        if (_.isEmpty(p.visual.order)) {
            p.play("Please, add something to your order first.");
        } else {
            p.play({command: 'highlight', id: 'time'});
            p.play("What is the delivery time?");
            p.then(date);
        }
    }
);

// checkout
intent(
    `That's (all|it)`,
    `(Ready to|) checkout`,
    p => {
        if (_.isEmpty(p.visual.order) || !p.visual.total) {
            p.play("Your cart is empty, please make an order first.");
            return;
        }
        p.play({command: 'navigation', route: '/cart'});
        p.play(`The total amount for your order is:`);
        p.play({command: 'highlight', id: 'total'});
        p.play(`${p.visual.total} dollars`);
        playDelivery(p, p.visual.address, p.visual.date, p.visual.time);
        p.then(checkout);
    }
);

intent(`Finish (order|)`, p => {
    if (_.isEmpty(p.visual.order)) {
        p.play("Please, add something to your order first");
    } else {
        p.play({command: 'finishOrder'});
    }
});

intent(
    `What is the total (price|amount) (of the order|for my order|)`,
    `How much is my order`,
    p => {
        if (p.visual.total && p.visual.total > 0) {
            p.play("The total amount for your order is:");
            if (p.visual.route === '/cart') {
                p.play({command: 'highlight', id: 'total'});
            }
            p.play(`${p.visual.total} dollars`);
        } else {
            p.play("Your cart is empty, please make an order first.")
        }
    }
);

intent(
    `(How much|what) does (the|) $(ITEM ${ITEMS_INTENT}) cost`,
    `How much is $(ITEM ${ITEMS_INTENT})`,
    p => {
        let order = p.visual.order || {};
        let price = ITEM_ALIASES[p.ITEM.value.toLowerCase()].price;
        let s = price !== 1 ? "s" : "";
        p.play(`${p.ITEM} (costs|is) ${price} dollar${s}`);
    }
);

intent(
    `Make the address $(LOC)`,
    `Set address to $(LOC)`,
    `Address (is|) $(LOC)`,
    p => {
        p.play({command: 'address', address: p.LOC.value});
        p.play({command: 'highlight', id: 'address'});
        p.play(`Delivery address is set to ${p.LOC}`);
    }
);

projectAPI.greet = (p, param, callback) => {
    p.play("Welcome to the Food Ordering demo app for food delivery. (How can I help you|What can I get for you|May I take your order|What would you like to order)?");
};
// Defining user's client ID and client secret keys
let clientId = "222b87964e954669b95ff25d3a05e53b";
let clientSecret = "13e4e8e784214e6aaf97005c96a3e7df";

const getAuth = async () => {
    try {
        const response = await api.axios({
            url: 'https://accounts.spotify.com/api/token',
            method: 'post',
            params: {
                grant_type: 'client_credentials'
            },
            headers: {
                'Accept':'application/json',
                'Content-Type': 'application/x-www-form-urlencoded'
            },
            auth: {
                username: clientId,
                password: clientSecret
            }
        });
        // Writing the access token to Alan Studio logs
        console.log(response.data.access_token);
        return response.data.access_token;
    } catch(error) {
        console.error(error);
    }
}
let tracksList = [];

const getTopTracks = async () => {
    // Getting the access token
    const access_token = await getAuth();
    // Defining the today's top list endpoint URL
    const api_url = "https://api.spotify.com/v1/playlists/37i9dQZF1DXcBWIGoYBM5M";
    try {
        const response = await api.axios.get(api_url, {
            // Sending the access token
            headers: {
                'Authorization': `Bearer ${access_token}`
            }
        });
        // Pushing the tracks names to the tracksList
        response.data.tracks.items.forEach(element => {
            tracksList.push(element.track.name);
        });
    } catch(error) {
        console.log(error);
    }
};
intent('What are the top 5 played songs on Spotify today?', async p => {
    // Getting the list of tracks
    await getTopTracks();
    // Naming the first 5 tracks
    p.play('The top 5 songs today are:');
    for (let i = 0; i < 5; i++) {
        let item = tracksList[i];
        p.play(`${item}`);
    }
})
