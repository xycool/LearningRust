# ∑ Difference of squares

25년 1월 14일(화) 🌥

https://exercism.org/tracks/rust/exercises/difference-of-squares

입력값이 10이라면 1부터 10까지의 합의 제곱과 각 수의 제곱의 합의 차이를 구하는 실습 문제다.

너무 쉬운거 아님? 😁

그동안 배웠던 map()과 fold()를 사용하면 간단하게 해결될 것 같아서 이렇게 만들어 봤다.

**내 버전**

```rust
pub fn square_of_sum(n: u32) -> u32 {
    (1..=n).sum::<u32>().pow(2)
}

pub fn sum_of_squares(n: u32) -> u32 {
    (1..=n).fold(0, |acc, x| acc + x.pow(2))
    
	// 아래 map과 sum을 사용하게 간단해 보인다.
	// (1..=n).map(|s| s.pow(2)).sum()
}

pub fn difference(n: u32) -> u32 {
    square_of_sum(n) - sum_of_squares(n)
}

fn main() {
    assert_eq!(square_of_sum(10), 3025);
    assert_eq!(sum_of_squares(10), 385);
    assert_eq!(difference(10), 2640);
}
```

이렇게 자신만만 할 때 커뮤니티 솔루션에는 아주 엄청난 버전이 있더란 말이지. 😳👽 외계인 아님? 강호 무림에는 엄청난 내공의 소유자들이 득실거린단 말이지. 졌다. 🙇‍♂️

👍👍외계인 버전 

수학의 등차수열과 자연수 제곱의 합의 개념으로 iterator를 사용하지 않고 해결한 버전 !!

https://exercism.org/tracks/rust/exercises/difference-of-squares/solutions/dfaligertwood

gemini에게 설명해 달라고 했다 😅 

https://docs.google.com/document/d/1mWX_VhwHPX5h7UpszrBKPlnpBa6114ApvlMWeieGC5E/edit?usp=sharing




