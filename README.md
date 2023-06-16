# lab9
<h1 align="center">МИНИСТЕРСТВО НАУКИ И ВЫСШЕГО ОБРАЗОВАНИЯ РОССИЙСКОЙ ФЕДЕРАЦИИ ФЕДЕРАЛЬНОЕ ГОСУДАРСТВЕННОЕ БЮДЖЕТНОЕ ОБРАЗОВАТЕЛЬНОЕ УЧРЕЖДЕНИЕ ВЫСШЕГО ОБРАЗОВАНИЯ «САХАЛИНСКИЙ ГОСУДАРСТВЕННЫЙ УНИВЕРСИТЕТ»</h1>
<p align="center">Лабораторная работа №6</p>
<p align="center">Лабораторная работа №8</p>
<p align="center">"JavaScript"</p>
<br>
<p align="right">Работу выполнил Гурков Владислав Викторович</p>
<p align="right">Работу проверил Соболев Евгений Игоревич</p>
### **Цели и задачи:**
Задачи:
1.	Есть некоторая строка (var str = 'fgfggg';), что будет, если мы возьмем str[0]?
2.	 Дана функция, она принимает в качестве аргументов строки '*', '1', 'b', '1c', реализуйте ее так, что бы она вернула строку '1*b*1c'
3.	Дано дерево, надо найти сумму всех вершин.
4.	Нарисовать стилями полукруг.
5.	Есть массив в котором лежат объекты с датами, отсортировать по датам.
6.	Есть несколько слов, определить состоят ли они из одних и тех же букв('кот', 'ток', 'окт')
7.	От них же. Числа от 1 до 100 лежат в массиве, они хаотично перемешанные, от туда изъяли одно число, надо найти, что это за число. алгоритм не должен превышать O(n^2) сложности.
8.	Реализовать сортировку пузырьком.
9.	Обратная польская нотация.
10.	Реализовать функцию является ли слово палендром.

```
function zz1(){ 
  
   var str="fgfggg"
   console.log(str[0])
}

function zz2(){
   var str1='*', str2 ='1', str3 ='b', str4 = '1c';
   console.log(str2 + str1 + str3 + str1 + str4)
}

function zz3(){ //дерево
	var sum = 0;

function getSum(obj) {
	sum += obj.valueNode;
	
	if (obj.next != null) {
		for (var i = 0; i < obj.next.length; i++) {
			getSum(obj.next[i]);
			
		}
	}

	return sum;
}


var tree = {
	valueNode: 3,
	next: [{
				valueNode: 1,
				next: null
			},
			{
				valueNode: 3,
				next: null
			},
			{
				valueNode: 2,
				next: null
			},
			{
				valueNode: 2,
				next: [
					{
						valueNode: 1,
						next: null
					},
					{
						valueNode: 5,
						next: null
					}
				]
			}]
};
console.log(getSum(tree));
}

function zz4(){
        
}

function zz5(){
        const arr = [];
        for (let i = 0; i < 10; i++) {
            arr[i] = { data: Math.floor(Math.random() * 31) }
        }
        console.log("Массив:", arr);
        sortedarr = [...arr].sort((a, b) => a.data - b.data);
        console.log("Отсортированный массив:", sortedarr);
}

function zz6(){
	function str(...words) {
        console.log("Слова:", words);
        let c = words[0].split('').sort().join('');

        for (let i = 1; i < words.length; i++) {
           if (c != words[i].split('').sort().join(''))
            return "не состоят из одних и тех же букв";
        }

        return "состоят из одних и тех же букв";
    }

    console.log(str("кот", "ток", "окт"));
}

function zz7(){
	const shuffle = [];
        for (let i = 0; i < 100; i++) {
            shuffle[i] = i + 1;
        }
    //Перемешивание массива
    for (let i = shuffle.length - 1; i > 0; i--) {
        let j = Math.floor(Math.random() * i);
        let temp = shuffle[i];
        shuffle[i] = shuffle[j];
        shuffle[j] = temp;
    }
    //Вырезаем случайный элемент
    let i = Math.floor(Math.random() * (shuffle.length - 1));
    shuffle.splice(i, 1);

    console.log("Перемешанный массив без одного элемента:", shuffle);

    //РЕШЕНИЕ:
    let seqSum = (1 + 100) / 2 * 100; // сумма арифм. прогрессии
    let arrSum = 0
    for (i in shuffle) {
        arrSum += shuffle[i];
    }
    console.log("В массиве изъяли число", seqSum - arrSum);
}

function zz8(){
	function bubbleSort(array) {
            let temp;
            for (let i = 0; i < array.length - 1; i++) {
                for (let j = 0; j < array.length - 1 - i; j++) {
                    if (array[j] > array[j + 1]) {
                        temp = array[j];
                        array[j] = array[j + 1];
                        array[j + 1] = temp;
                    }
                }
            }
        } 
        const mas = [];
        for (let i = 0; i < 10; i++) {
            mas[i] = Math.floor(Math.random() * 20) - 10;
        }
        console.log("Дан массив:", mas);
        bubbleSort(mas);
        console.log("Отсортированный пузырьком массив:", mas)
}

function zz9(){
	 function reversPolNot(string) {
            let infix = string.replace(/\s/g, '').split('');
            let postfix = [], stack = [];
            let priority = 3;

            for (i in infix) {
                switch (infix[i]) {
                    case '(':
                        stack.push(infix[i]);
                        priority = 3;
                        break;
                    case ')':
                        do {
                            postfix.push(stack.pop());
                        } while (stack[stack.length - 1] != '(');
                        stack.pop();
                        priority = 3;
                        break;
                    case '^':
                        stack.push(infix[i]);
                        priority = 1;
                        break;
                    case '*':
                    case '/':
                        if (priority < 2)
                    do {
                        postfix.push(stack.pop());
                    } while (stack[stack.length - 1] != '(' && stack.length != 0);
                        stack.push(infix[i]);
                        priority = 2;
                        break;
                    case '+':
                    case '-':
                        if (priority < 3)
                        do {
                            postfix.push(stack.pop());
                        } while (stack[stack.length - 1] != '(' && stack.length != 0);
                    stack.push(infix[i]);
                    priority = 3;
                    break;
                default:
                    postfix.push(infix[i]);
                    break;
                }
            }

        for (i in stack) {
            postfix.push(stack.pop());
        }

    return postfix.join('');
	}

    const stroka = "(8 + 2 * 5) / 2 + 3 / 4 - 5 ^ 3 + ( 1 + 3 * 2 - 4)";
    console.log("Постфиксная:", stroka);
    console.log("Обратная польская:", reversPolNot(stroka));
}

function zz10(){
	
	function Palindrome(word) {
            if (word == "")
            return "";

            if (word.length == 1)
            return "Не палиндром";

            word = word.toLowerCase();
            for (let i = 0; i < word.length / 2; i++) {
                if (word[i] != word[word.length - 1 - i])
                return "Не палиндром"
            }

        return "Палиндром";
    }

    let word = "Шалаш";
    console.log("Слово: ", word);
    console.log(Palindrome(word));
}
```
### **Вывод:**
После выполнения данной лабораторной работы я улучшил свои навыки работы с JavaScript.
