# physicalexamination

# 평균 키의 값과 시력 분포를 구하는 알고리즘
<br><br>
### JAVA 코드
------------------
``` java
	static final int VMAX = 21;
	
	static class PhyscData {
		
		String name;
		int height;
		double vision;
		
    PhyscData(String name, int height, double vision) { \\  클래스의 생성자를 정의하는 코드이다. 이 생성자는 String, int, double 형태의 name, height, vision을 가진다.
				
			this.name = name;         \\ this 키워드를 사용하여 클래스의 멤버 변수에 매개변수 값을 할당하고 있다. 
			this.vision = vision;
			this.height = height;
	
		}
	}
	
	static double aveHeight (PhyscData[] dat) { \\ PhyscData 배열을 입력받아 배열에 있는 사람들의 평균 키를 계산하여 반환하는 정적 메서드이다.
		double sum = 0;
		
		for (int i = 0; i < dat.length; i++)	\\ 사람 수 만큼 for문을 반복해 sum값에 키 수치를 누적해준다.
			sum += dat[i].height;               \\ sum 값에 현재 키의 값을 누적한다.
		return sum / dat.length;	            \\ 누적된 sum값 ÷ 사람 수)를 보내준다.
	}
	\\ 시력의 분포 구하기
	static void distVision (PhyscData[] dat, int[] dist) {  \\ 시력값을 받아서 시력 범위에 따른 빈도수를 계산하여 배열에 저장하는 메소드이다. 
		int i = 0;
		dist[i] = 0;
		for (i=0; i<dat.length; i++)  
			if (dat[i].vision >= 0.0 && dat[i].vision <= VMAX / 10.0 ) 
				dist[(int)(dat[i].vision * 10)]++;
	}

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		
		PhyscData [] x = {
			new PhyscData("강민하", 162, 0.3),
			new PhyscData("김찬우", 173, 0.7),
			new PhyscData("강민하", 175, 2.0),
			new PhyscData("강민하", 171, 1.5),
			new PhyscData("강민하", 168, 0.4),
			new PhyscData("강민하", 174, 1.2),
			new PhyscData("강민하", 169, 0.8),
		};
		
		int [] vdist = new int [VMAX];
		
		System.out.println("■ 신체검사 리스트 ■");
		System.out.println("이름	키	시력");
		System.out.println("------------------");
		
		for (int i=0; i<x.length; i++)
			System.out.printf("%-6s%3d%5.1f\n",x[i].name, x[i].height, x[i].vision);
		System.out.printf("\n평균 키: %5.1fcm\n", aveHeight(x));
		
		distVision (x, vdist);
		System.out.println("\n시력 분포");
		for (int i=0; i<VMAX; i++)
			System.out.printf("%3.1f ~ : %2d명\n", i / 10.0, vdist[i]);
	
}
```
<br><br><br><br><br>
### 인원 수
------------------
![image](https://user-images.githubusercontent.com/114748816/225799264-55731919-1627-4dbd-96df-dfa0df12b044.png)  <br><br>
상수를 정의하는 방법 중 하나인 static final을 사용하여 VMAX라는 이름의 정수형 상수를 선언하고 초기값으로 21을 할당한 것이다.
<br><br><br><br><br>

### 클래스 생성자
------------------
![image](https://user-images.githubusercontent.com/114748816/225799980-7462c28a-f0c8-491b-8757-40a7ea0a54eb.png) <br><br>
PhyscData 클래스의 생성자는 String name, int height, double vision 이라는 3개의 매개변수를 가지며, <br><br>
이를 통해 객체가 생성될 때 해당 객체의 name, height, vision 멤버 변수에 값을 할당한다. <br><br><br><br><br>

### 키 평균
------------------
![image](https://user-images.githubusercontent.com/114748816/225800613-d287e1b3-e9c8-474b-884d-4516d41bafd5.png) <br><br>
sum의 값을 0으로 초기화 하고,<br><br>
i의 값이 dat 배열의 길이 보다 작다면 i값을 증가시켜,<br>
i의 값이 배열의 길이와 같을때까지 실행시켜 준다. <br><br>
sum 값에 현재 dat 배열에 있는 키의 값을 더해 누적시켜 준다. <br><br>
누적된 sum값 ÷ dat 배열의 길이)의 값을 main 매서드로 보내준다. <br><br><br><br><br>

### 시력 분포
------------------
![image](https://user-images.githubusercontent.com/114748816/225802488-b7702313-90ee-4d9f-87a8-c6e1bdd31f4f.png) <br><br>
여기서 VMAX는 최대 시력 값이며, 시력은 0.0부터 VMAX까지의 값으로 표현한다. <br><br>
시력 값을 0.1 단위로 나누어서 각 범위에 해당하는 인덱스를 구하고, <br><br>
해당 인덱스에 대응하는 배열 요소(dist[])의 값을 1씩 증가시킨다.	<br><br><br><br><br>

### 출력
------------------
![image](https://user-images.githubusercontent.com/114748816/226500449-48d5eff0-05bb-4a32-a430-3a6f0c4114e0.png) <br><br>
printf() 함수를 이용하여 출력 형식을 지정하고, %s, %d, %f의 서식 지정자를 이용하여 문자열, 정수, 실수 값을 출력해준다. <br><br>
aveHeight() 함수는 평균 키를 계산하여 반환하는 함수이다. <br><br>
함수의 인자로 배열 x를 전달하고 있으며, 배열의 각 요소의 키 정보를 더한 후 배열의 길이로 나누어 평균 값을 계산하고 있다. <br><br>

