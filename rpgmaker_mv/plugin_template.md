---
layout: page
title: 플러그인 기본틀
---


### 플러그인 기본 샘플 코드


~~~ js 
//=============================================================================
/*
 * //플러그인 설명
 * @plugindesc 테스트 플러그인 입니다.
 * 플러그인 설명 두번째 줄
 *
 * @author name
 *
 * @param test value
 * @desc 테스트 파라미터1
 * 기본값 : 100    
 * @default 100
 *
 * @param test_value2
 * @desc 테스트 파라미터2
 * @default 200
 */
//=============================================================================
~~~

플러그인 매니져 플러그인 설명과 파라미터 값을 설정해 주는 코드.

~~~ js 
(function() {

	//플러그인 파일 이름
	var parameters = PluginManager.parameters('test_plugin');

	//플러그인 파라미터 불러오기
	var test_value = Number(parameters['test value'] || 100);	
	var test_value2 = Number(parameters['test_value2'] || 200);	

	//플러그인 명령 처리 클래스 상속
	var _Game_Interpreter_pluginCommand = Game_Interpreter.prototype.pluginCommand;
	Game_Interpreter.prototype.pluginCommand = function(command, args) {
		_Game_Interpreter_pluginCommand.call(this, command, args);
		command = command.toLowerCase();
		
		//플러그인 명령 처리 추가
		//testcommand 11 22 33 aa 
		if (command === 'testcommand') 
		{			
			alert(test_value);
			alert(test_value2);
			
			//플러그인 인자
			alert(args[0]);
			alert(args[1]);
			alert(args[2]);
			alert(args[3]);
			alert(args[4]);
		}
	}

})(); // end
~~~

플러그인 매니져에서 사용자가 고친 파라미터 값을 불러 옵니다.

이벤트의 플러그인 명령에서 입력한 명령에 따라서 작동하는 코드를 추가 해 줍니다.
