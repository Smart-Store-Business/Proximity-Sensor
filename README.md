# Proximity Sensor Firmware
Proximity-Sensor for CDU

## 개요
* 새로운 근접센서는 이전 버전의 센서와는 달리 센서와 대상물 간의 거리가 아니라 대상물의 움직임을 인식한다.
* 가까이 있더라도 움직이지 않으면 반응하지 않는다. 반면, 어느 정도 멀리에 있어도 움직임이 큰 경우에는 반응한다. 현재 약 2m 정도 이내의 움직임에는 반응하도록 설정되어 있다.
* 센서는 0.25초에 한번씩 센서 앞쪽의 움직임을 체크하여 그 값을 하나의 숫자로 만든다. 이를 movement값으로 지칭하도록 한다.
* 센서 앞쪽에 아무것도 없어도 movement값은 25 ~ 50 정도를 왔다 갔다한다. 
* 센서가 정해진 Threshold보다 큰 움직임을 감지하면 그 movement값을 serial로 출력한다. 디폴트는 100이다. 즉, 100이하의 movement값은 출력되지 않고 100이상인 movement값은 출력된다.

## 시작
* serial 포트를 115200, no parity, no flow control로 연다.
* "M:Ready\n"라는 문자열을 기다려서 수신한다.
* serial 포트를 open한 후 "M:Ready\n"가 수신될 때까지의 시간은 약 5초 정도이다.
* 센서 앞쪽에서 손을 흔들거나 하면 "M:153\n"과 같은 포맷으로 movement값이 출력될 것이다.

## 데이터의 포맷
* 모든 데이터는 ascii 코드로 출력되고 newline 문자는 LF만 사용한다.
* movement값은 최대 4자리까지 출력될 수 있다.
* 대상물의 움직임이 일정 크기 이상 계속되면 movement값이 계속 출력된다. 1초에 최대 4번까지 출력된다.

## sensor 제어 기능
* 센서를 제어할 수 있는 여러가지 기능이 존재한다. (필요시 문의 바랍니다.)
 * movement값의 출력을 On / Off
 * 출력되는 movement값의 Threshold를 변경
 * 센서로 접근하는 경우에만 반응하도록 센서의 동작 인식 알고리듬을 변경
 * RF 파워를 변경
