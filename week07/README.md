## LedToggle.cpp
```
#include "LedToggle.h"

LedToggle::LedToggle(int pin){
	_pin = pin;
	_state = false;
	_delayTime = 0;//이 부분이 중요함. 놓칠수도 있는 부분. ...작동하는 법에 따라 수를 다르게 입력할 수 있음.
				//아두이노에서 선언을 안하면 해당 숫자가 기본값으로 실행됨.
	pinMode(_pin, OUTPUT);//아두이노 헤더를 인클루드 했기 때문에 같이 쓸 수 있음 
	digitalWrite(_pin, LOW);
}
LedToggle::LedToggle(int pin, unsigned long delayTime) {
	_pin = pin;
	_state = false;
	_delayTime = delayTime;
	pinMode(_pin, OUTPUT);
	digitalWrite(_pin, LOW);
}


void LedToggle::toggle(){

	if (_delayTime > 0){
	delay(_delayTime);//delayTime의 기본값을 넣어주는 작업이 필요함
	}

	_state = !_state;
	digitalWrite(_pin, _state ? HIGH : LOW);
}
```
##LedToggle.h
```
#ifdef LedToggle_h
#defiine LedToggle_h

#include "Arduino.h"

class LedToggle {
public:
	LedToggle(int pin);
	void toggle();

private:
	int _pin;
	bool _state;
};

#endif
```
```
#ifdef LedToggle_h
#defiine LedToggle_h

#include "Arduino.h"

class LedToggle {
	public:
		LedToggle(int pin);
		LedToggle(int pin, unsigned long delatTime);
		void toggle();
	
	private:
		int _pin;
		bool _state;
			unsigned long _delayTime;
};

#endif
```
