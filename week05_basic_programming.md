---
layout: default
title: "Getter, Setter 예제"
---

> ## Getter, Setter 예제
> TODO 부분을 완성해주시면 됩니다
>
> TODO 부분은 클래스 Final 내부의 calcFinalScore()메소드에 있습니다.
>

```java
class Course {
	private int score = 0;
	private int finalScore = 0;
	public Course(int score) {
		this.score = score;
	}
		
	public void setCourse(int inputScore) {
		score = inputScore;
	}
	public int getScore() {
		return score;
	}
	public void setFinalScore(int inputScore) {
		finalScore = inputScore;
	}
	public int getFinalScore() {
		return finalScore;
	}
}
class Midterm {
	private Course[] scoreInformation;
	Midterm(int numOfCourse) {
		scoreInformation = new Course[numOfCourse];
	}
	public Course[] getScoreInformation() {
		return scoreInformation;
	}
	public void setScoreInformation(Course[] scoreInformation) {
		this.scoreInformation = scoreInformation;
	};
}
class Final {
	// 중간성적과 기말성적을 기반으로 합산 성적을 계산하는 메소드입니다. 완성해주세요
	public void calcFinalScore(Course[] midScore, int[] finalScore) {
		// TODO ===========================================
		// 순서 1. midScore에 저장된 객체들을 for문을 통해 불러옵니다
		// 순서 2. for문 내부에서 Course의 getScore을 통해, midScore의 객체들로부터 중간고사 점수 score을 받아오세요
		// 순서 3. finalScore으로부터 기말 점수를 받아오세요
		// 순서 4. 받은 기말고사 성적과 중간고사 성적의 평균을 냅니다.
		// 순서 5. 계산된 평균을 setFinalScore을 통해 각 Course객체에 저장해주세요
		//       ===========================================
		
		System.out.println("------ 기말 합산 결과 ------");
		printResult(midScore);
	}
	
	// 출력을 위한 메소드입니다
	public void printResult(Course[] result) {
		int sumMid = 0;
		int sumFinal = 0;
		for(int i=0;i<result.length;i++) {
			sumMid += result[i].getScore();
			sumFinal += result[i].getFinalScore();
			System.out.println("중간은 "+result[i].getScore()+", 기말 합산 결과는 "+result[i].getFinalScore());
		}
		System.out.println("중간 총 합은 : "+sumMid+", 기말 합산 결과는 "+sumFinal);
	}
}
public class Main {
	
	public static void main(String[] args) {
		// 목표 : Final class의 calcFinalScore을 완성해 아래의 코드가 정상적으로 작동하도록 만들어주세요
		
		// 성적은 다음과 같습니다
		//	중간고사  	             컴퓨터개론         데이터베이스       알고리즘	      네트워크개론	
		Course[] mid = new Course[] { new Course(23), new Course(40), new Course(50), new Course(17)};
		//	기말고사	             컴퓨터개론         데이터베이스       알고리즘	      네트워크개론	
		int[] finalScore = new int[] {      45,            78,             99,               50     };
		
		// Midterm클래스의 객체인 myMid에 중간고사 성적을 넣었습니다
		 Midterm myMid = new Midterm(4);
		 myMid.setScoreInformation(mid);

		//  Midterm의 객체와 finalScore을 calcScore()을 활용해서 기말 합산 결과를 출력
		 new Final().calcFinalScore(myMid.getScoreInformation(), finalScore);
	}

}
```

> 현재 출력

```
------ 기말 합산 결과 ------
중간은 23, 기말 합산 결과는 0
중간은 40, 기말 합산 결과는 0
중간은 50, 기말 합산 결과는 0
중간은 17, 기말 합산 결과는 0
중간 총 합은 : 130, 기말 합산 결과는 0
```

> 예상 출력

```
------ 기말 합산 결과 ------
중간은 23, 기말 합산 결과는 34
중간은 40, 기말 합산 결과는 59
중간은 50, 기말 합산 결과는 74
중간은 17, 기말 합산 결과는 33
중간 총 합은 : 130, 기말 합산 결과는 200
```

> 답안
	
```java
class Course {
	private int score = 0;
	private int finalScore = 0;
	public Course(int score) {
		this.score = score;
	}
		
	public void setCourse(int inputScore) {
		score = inputScore;
	}
	public int getScore() {
		return score;
	}
	public void setFinalScore(int inputScore) {
		finalScore = inputScore;
	}
	public int getFinalScore() {
		return finalScore;
	}
}
class Midterm {
	private Course[] scoreInformation;
	Midterm(int numOfCourse) {
		scoreInformation = new Course[numOfCourse];
	}
	public Course[] getScoreInformation() {
		return scoreInformation;
	}
	public void setScoreInformation(Course[] scoreInformation) {
		this.scoreInformation = scoreInformation;
	};
}
class Final {
	// 중간성적과 기말성적을 기반으로 합산 성적을 계산하는 메소드입니다. 완성해주세요
	public void calcFinalScore(Course[] midScore, int[] finalScore) {
		// TODO ===========================================
		// 순서 1. midScore에 저장된 객체들을 for문을 통해 불러옵니다
		// 순서 2. for문 내부에서 Course의 getScore을 통해, midScore의 객체들로부터 중간고사 점수 score을 받아오세요
		// 순서 3. finalScore으로부터 기말 점수를 받아오세요
		// 순서 4. 받은 기말고사 성적과 중간고사 성적의 평균을 냅니다.
		// 순서 5. 계산된 평균을 setFinalScore을 통해 각 Course객체에 저장해주세요
		//       ===========================================
		for(int i=0;i<midScore.length;i++) {
			midScore[i].setFinalScore((midScore[i].getScore() + finalScore[i])/2);
		}
		
		System.out.println("------ 기말 합산 결과 ------");
		printResult(midScore);
	}
	
	// 출력을 위한 메소드입니다
	public void printResult(Course[] result) {
		int sumMid = 0;
		int sumFinal = 0;
		for(int i=0;i<result.length;i++) {
			sumMid += result[i].getScore();
			sumFinal += result[i].getFinalScore();
			System.out.println("중간은 "+result[i].getScore()+", 기말 합산 결과는 "+result[i].getFinalScore());
		}
		System.out.println("중간 총 합은 : "+sumMid+", 기말 합산 결과는 "+sumFinal);
	}
}
public class Answer {
	
	public static void main(String[] args) {
		// 목표 : Final class의 calcFinalScore을 완성해 아래의 코드가 정상적으로 작동하도록 만들어주세요
		
		// 성적은 다음과 같습니다
		//	중간고사  					컴퓨터개론		   데이터베이스		알고리즘			네트워크개론				
		Course[] mid = new Course[] { new Course(23), new Course(40), new Course(50), new Course(17)};
		//	기말고사  					컴퓨터개론		   데이터베이스		알고리즘			네트워크개론				
		int[] finalScore = new int[] {      45,            78,             99,               50     };
		
		// Midterm클래스의 객체인 myMid에 중간고사 성적을 넣었습니다
		 Midterm myMid = new Midterm(4);
		 myMid.setScoreInformation(mid);

		//  Midterm의 객체와 finalScore을 calcScore()을 활용해서 기말 합산 결과를 출력
		 new Final().calcFinalScore(myMid.getScoreInformation(), finalScore);
	}

}
```
