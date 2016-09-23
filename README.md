# AnswerFront
<script type="text/javascript">
//Fuzbuz задачи. Задача 1
"use strict";
function dscount(str, s1, s2)
{
	str = str.toUpperCase();
	s1 = s1.toUpperCase();
	s2 = s2.toUpperCase();
	
	var n;
	var l = str.length;
	var count = 0;
	for (n=0; n < l; ++n)
	{
		if ((str[n] == s1) && (str[ n + 1 ] == s2))
		{
			count = count + 1;
		}
	}
	return count;
}
// Для удобства можно использовать эти тесты:
try {
    test(dscount, ['ab___ab__', 'a', 'b'], 2);
	test(dscount, ['___cd____', 'c', 'd'], 1);
    test(dscount, ['de_______', 'd', 'e'], 1);
    test(dscount, ['12_12__12', '1', '2'], 3);
    test(dscount, ['_ba______', 'a', 'b'], 0);
    test(dscount, ['_a__b____', 'a', 'b'], 0);
    test(dscount, ['-ab-аb-ab', 'a', 'b'], 2);
    test(dscount, ['aAa', 'a', 'a'], 2);

    console.info("Congratulations! All tests success passed.");
} catch(e) {
    console.error(e);
}
// Простая функция тестирования
function test(call, args, count, n) {
    let r = (call.apply(n, args) === count);
    console.assert(r, `Finded items count: ${count}`);
    if (!r) throw "Test failed!";
}

//==============================================================================\///Задача 2

function checkSyntax(string)
{
    var n;
    var l = string.length;
    var stack = [];
    var ob = {'<': '>', '(': ')', '[': ']', '{': '}'};
    var cb = {'>': '<', ')': '(', ']': '[', '}': '{'};

    var char;
    var br;


    for (n=0; n < l; n++)
    {
        char = string.charAt(n);
        if(ob[char])
        {
            stack.push(char);
        }
        else
        if(cb[char])
        {
            if(( stack.length == 0 ) || ( ob[stack[stack.length - 1]] != char ))
                return 1;

            stack.pop();
        }
    }
    return stack.length == 0 ? 0 : 1;
}	



if(! (checkSyntax("---(++++)----") == 0))
    alert("1");
    
if(! (checkSyntax("") == 0))
    alert("2");

if(! (checkSyntax("before ( middle []) after ") == 0))
    alert("3");

if(! (checkSyntax(") (") == 1))
    alert("4");

if(! (checkSyntax("} {") == 1))
    alert("5");

if(! (checkSyntax("<(   >)") == 1))
    alert("6");

if(! (checkSyntax("(  [  <>  ()  ]  <>  )") == 0))
    alert("7");

if(! (checkSyntax("   (      [)") == 1))
    alert("8");

//==============================================================================
//АЛГОРИТМЫ Задача 1
//Задача про блинчики

/*
Для жарки 3х блинчиков на 2х сковородках необходимо 3 мин.
Обозначим блины буквами a, b, c
Обозначим стороны блина цифрами 1,2

Жарим в след. последовательности:

1. a1 & b1 = 1мин 
2. b2 & c1 = 1мин 
3. c2 & a2 = 1мин 
    
        Итого: 3 мин.
        
Применен алгоритм конвеера.
Т.е. более сложная задача (обжарка с 2х сторон) разбита на 2 стадии (2 стороны и 2 сковороды).
На каждой итерации обжариваеться 2 блина на каждой сковороде, что позволяет сократить время.
*/

//РЕФАКТОРИНГ Задача 1

function func(s, a, b) {

    if (s.match(/^$/)) {
        return -1;
    }

    var i = s.length -1;
    var aIndex =     -1;
    var bIndex =     -1;

    while ((aIndex == -1) && (bIndex == -1) && (i > 0)) {
        if (s.substring(i, i +1) == a) {
            aIndex = i;
        }
        if (s.substring(i, i +1) == b) {
            bIndex = i;
        }
        i = i - 1;
    }

    if (aIndex != -1) {
        if (bIndex == -1) {
            return aIndex;
        }
        else {
            return Math.max(aIndex, bIndex);
        }
    }

    if (bIndex != -1) {
        return bIndex;
    }
    else {
        return -1;
    }
}

//Замена для func
function func2(s, a, b)
{
    var i;

    for (i = s.length; i > 0; --i)
    {
        if ((s[i] == a) || (s[i] == b))
        {
            return i;
        }
    }
    return -1;
}

if( func("qwerty", 'e', 't') != func2("qwerty", 'e', 't') )
    alert('1');

if( func("qwerty", 't', 'w') != func2("qwerty", 't', 'w') )
    alert('2');

if( func("qwerty", 't', 't') != func2("qwerty", 't', 't') )
    alert('3');

if( func("qwerty", 'z', 'z') != func2("qwerty", 'z', 'z') )
    alert('4');

if( func("qwerty", 'z', 'r') != func2("qwerty", 'z', 'r') )
    alert('5');

if( func("qwerty", 'r', 'z') != func2("qwerty", 'r', 'z') )
    alert('6');

//==============================================================================
//Задача 2
function drawRating(vote) {
    return (vote / 20 | 0 ) + 1;
}
// Проверка работы результата
console.log(drawRating(0) ); // ★☆☆☆☆
console.log(drawRating(1) ); // ★☆☆☆☆
console.log(drawRating(50)); // ★★★☆☆
console.log(drawRating(99)); // ★★★★★


//==============================================================================
//Практические задачи. Задача 1

function parseUrl(url)
{
    var elem = document.createElement('a');
    elem.href = url;
    return elem;
}

let a = parseUrl('http://tutu.ru:8080/do/any.php?a=1&b[]=a&b[]=b#foo')

// Вернет объект, в котором будут следующие свойства:
console.log( a.href == "http://tutu.ru:8080/do/any.php?a=1&b[]=a&b[]=b#foo" )
console.log( a.hash == "#foo" )
console.log( a.port == "8080" )
console.log( a.host == "tutu.ru:8080" )
console.log( a.protocol == "http:" )
console.log( a.hostname == "tutu.ru" )
console.log( a.pathname == "/do/any.php" )
console.log( a.origin == "http://tutu.ru:8080" )

</script>
