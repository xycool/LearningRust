# 🌾 Grains

25년 1월 16일(목) 

https://exercism.org/tracks/rust/exercises/grains

어느 나라의 왕이 왕자의 생명을 구한 현명한 하인에게 가지고 싶은걸 말하라고 한다. 왕이 체스를 좋아한다는걸 알고 있기도 하고 하인은 밀알을 먹고 싶다고 말하면서 .... 체스보드상의 각 보드에는 앞에 보드위에 있는 밀알의 2배가 있다는 가정하에 64 체스보드에는 전체 밀알의 개수가 몇개인지 구현하는 실습과제다.

이것도 그렇게 어렵지 않다.

**내 버전**

```rust
pub fn square(s: u32) -> u64 {
	// 2_u64로 해줘야 함.
	2_u64.pow(s - 1)
}

pub fn total() -> u64 {
    (1..=64).map(square).sum()
}

fn main() {
	assert_eq!(square(1), 1);
	assert_eq!(square(64), 9_223_372_036_854_775_808);
	assert_eq!(total(), 18_446_744_073_709_551_615);
}
```



👍👍비트연산 버전  

비트연산을 이용한 아주 심플한 버전 !!

https://exercism.org/tracks/rust/exercises/grains/solutions/soxfox42

gemini의 설명 🙋‍♂️

https://g.co/gemini/share/699ef6bb8d85








