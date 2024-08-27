
# 드림핵 rev-basic-1 WriteUP
워게임 주소: https://dreamhack.io/wargame/challenges/15/

## 동적 분석

### 프로그램 실행시켜 보기

<img width="683" alt="스크린샷 2024-08-27 오후 7 14 46" src="https://github.com/user-attachments/assets/014145ed-eec7-49e2-a1ee-9e6763c2857e">

#### 동적 분석 결과

- Input이라는 문자열과 함께 사용자 입력 값을 받는다.
- 사용자 입력 값이 특정 문자열이 아니면 Wrong 이라는 문자열을 출력한다.

## 정적 분석

### IDA에 파일 로드 하기

<img width="630" alt="스크린샷 2024-08-27 오후 7 17 33" src="https://github.com/user-attachments/assets/a83406bf-c79d-4793-a108-cb305f84943b">

### IDA 자동 main 함수 찾기 기능

아래 그림과 같이 IDA에서 main함수를 자동으로 찾아 주는 것을 볼 수 있다.

<img width="567" alt="스크린샷 2024-08-27 오후 7 21 22" src="https://github.com/user-attachments/assets/d8094bfd-c0b7-48b0-a37f-1dca9a6de409">

### main 함수 Decompile

main 함수를 클릭하고 f5를 눌러 디컴파일을 진행한다.

<img width="563" alt="스크린샷 2024-08-27 오후 7 23 38" src="https://github.com/user-attachments/assets/58b2aadd-e189-423c-9dff-05d8bd9daeaa">

디컴파일 결과 동적 분석한 결과와 같이 scanf함수와 printf 함수가 있다는 것을 유추 할 수 있다.
또한 if문에 printf함수가 있는 것을 보아 특정 문자열일 경우 Correct를 출력하는 로직임을 알 수 있다.

sub_140001190 => printf 함수 유추
sub_1400011F0 => scanf 함수 유추
sub_140001000 => 사용자 입력 값 특정 문자열과 비교하는 함수 유추 (일치하면 Correct, 불일치 시 Wrong)

### sub_140001190 함수 정적 분석

아래 그림과 같이 arct_iob_func(1u)는 stdout 파일스트림을 가져와 sub_140001060으로 전달 한 것을 볼 수 있다.
<img width="493" alt="스크린샷 2024-08-27 오후 7 27 24" src="https://github.com/user-attachments/assets/d849cb85-ca10-4e11-b89c-b32ef1f2e301">

아래 그림은 sub_140001060함수로 printf 함수임을 알 수 있다.

<img width="679" alt="스크린샷 2024-08-27 오후 7 31 43" src="https://github.com/user-attachments/assets/654b4053-c45b-494a-9720-db377de5cd26">

### sub_1400011F0

아래 그림과 같이 arct_iob_func(0)는 stdin 파일스트림을 가져와 sub_1400010B0으로 전달 한 것을 볼 수 있다
<img width="488" alt="스크린샷 2024-08-27 오후 7 34 19" src="https://github.com/user-attachments/assets/e091c0fa-6e10-4ec7-afe0-12a4e2ca38bd">


아래 그림은 sub_1400010B0함수로 scanf 함수임을 알 수 있다.
<img width="688" alt="스크린샷 2024-08-27 오후 7 36 39" src="https://github.com/user-attachments/assets/f34f55fd-1797-45f1-a225-fc8f77cf023e">



### sub_140001000

sub_140001000를 더블클릭하여 디컴파일된 함수를 보아, 사용자 입력 값과 "Compar3_the_str1ng"값이 같은지 비교하는 함수인 것을 알 수 있다.


<img width="378" alt="스크린샷 2024-08-27 오후 7 38 08" src="https://github.com/user-attachments/assets/f321d9bc-9fa5-471a-9647-1a522565e382">

### Debugging

<img width="519" alt="스크린샷 2024-08-27 오후 7 40 51" src="https://github.com/user-attachments/assets/b2d7655e-023c-4a35-ba15-442e16b1c0f3">

메인함수에서 f4를 눌러 디버깅을 진행하여 사용자 입력 값을 "Compar3_the_str1ng"로 입력한다.

<img width="276" alt="스크린샷 2024-08-27 오후 7 47 38" src="https://github.com/user-attachments/assets/178c116f-858b-422f-a24f-4d64ef548a4d">



















