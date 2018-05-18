# IPUI-IPEI
Конвертация IPUI в IPEI



<!DOCTYPE html>
<html>
    <head>
	<meta charset="utf-8">
	<title>Конвертация из IPUI в IPEI</title>
	</head>
    <body bgcolor="#FBE2FF">
      <!--    <span style="color: red"; font-size: 2em">L</span> -->
		 <p style="text-align:center"> 
             <br><br><br><br><br><br><br>
             <span style="color: gray; font-size: 1.5em">Конвертация IPUI в IPEI</span>
			 <br><br>
		     <input type='text' autofocus placeholder="Введите IPUI" id='userInput' size=10>
             <button onClick="userSubmit()">Конвертация</button>
             <br>
             <div style="text-align:center" id='result'></div>
		 </p>
         <script  type="text/javascript">
               function userSubmit() {
        
		       //переменной IPUI присвоить введенное значение
		       var IPUI=document.getElementById('userInput').value;
		
			  //Убрать пробелы если имеются
			  IPUI = IPUI.replace(/\s/g, '');
			  			  			  
		      //Защита от дурака 1
			  var InputError = false; // пока что нет ошибок ввода данных пользователем
			  //Проверить на правильность ввода - должно быть 10 символов
			  str = IPUI.length;
			  if (str != 10) {
		      InputError = true;
			  alert( 'Ошибка ввода IPUI! Неверное количество символов' );
		      }
              //Защита от дурака 2
			  //Проверка на ввод шестнадцатеричных символов при вводе IPUI
			  var x = "";
			  if (InputError == false) {
			  for (var a = 0; a < 10; a++) {
			     x = IPUI.charAt(a);
			     if (x == 0 || x == 1 || x == 2 || x == 3 || x == 4 || x == 5 || x == 6 || x == 7 || x == 8 || x == 9 || x == "a" || x == "b"  || x == "c"  || x == "d"  || x == "e"  || x == "f" || x == "A" || x == "B"  || x == "C"  || x == "D"  || x == "E"  || x == "F" ) {
		            //alert( 'Правильный ввод IPUI!' );
		         } else {
  				        InputError = true;
						a = 10; //выход из цикла 
						alert( 'Ощибка ввода IPUI! Должны быть только шестнадцатеричные символы' );
			     }
			  }  //end for
			  } //end if
			  //Вывести в поле ввода введенное значение без пробелов
		      document.getElementById('userInput').value = IPUI;
			  //Если пользователь не совершил ошибок при вводе идем дальше, иначе стоп. 
			  if (InputError == false) {	
			  //обрезать первый символ в переменной IPUI
			  var str = IPUI;
			  IPUI = str.substr(1);
		
			  //ECM - первые 4 символа 
			  var ECM = IPUI.substr(0, 4);
        
			  //PSN - с 5 по 9 символ
			  var PSN = IPUI.substr(4, 9);
		
			  //перевод из 16 в 10
			  str = parseInt(ECM, 16);
			  ECM = str;
			  str = parseInt(PSN, 16);
			  PSN = str;
		
			  // Добавить 0 в начало PSN
			  str = "0" + PSN;
			  PSN = str;
		
			  //Объединение ECM и PSN = ECMPSN
			  str = ECM + PSN;

			  //Добавить в массив arr значения по символам
			  var arrA = [];
			  for (var i = 0; i < 12; i++) {
              arrA[i]=str.substr(i, 1);
              }
		
		      // В MassC вбить значения от 1 до 12
              var arrB = [];
	      	  for (var i = 1; i < 13; i++) {
              arrB[i-1]= i;
              }
		
	       	 //Перемножить 
		      var Summa = 0;
		      for (var i = 0; i < 12; i++) {
              Summa =  Summa + (arrA[i] * arrB[i]);
              }

		      //Остаток от деления		
		      Summa = Summa % 11;
		
		      if (Summa == 10) {
		      Summa = '*';
		      }
		      //добавление модуло в конец str
		      str = str + Summa;
			  
	          //вывод на экран
		      document.getElementById('result').innerHTML='IPEI: '+ str;
			  } else { document.getElementById('result').innerHTML='IPEI: расчитать не возможно';
                     document.getElementById('userInput').focus(); //Установить курсор на поле ввода
			         document.getElementById('userInput').select();	//Выделить текст на поле ввода
					 }
              } //конец функции
</script>

    </body>
</html>


