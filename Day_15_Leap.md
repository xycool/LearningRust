# 🗓 Leap

25년 1월 20일(월) 

https://exercism.org/tracks/rust/exercises/leap

특정 년도를 인풋값으로 주면 해당 년도가 윤년에 해당하는지 구현하는 과제다.

## 윤년

- 윤년에 대해서는 나무위키를 참고하자 (https://namu.wiki/w/%EC%9C%A4%EB%85%84)

**내 버전**

```rust
pub fn is_leap_year(year: u64) -> bool {
	(year % 4 == 0 && year % 100 != 0) || year % 400 == 0
}
```

match를 사용한 커뮤니티 솔루션 버전도 참고하자.

https://exercism.org/tracks/rust/exercises/leap/solutions/steveklabnik











