# Armstrong Numbers

25년 1월 11일

[https://exercism.org/tracks/rust/exercises/armstrong-numbers](https://exercism.org/tracks/rust/exercises/armstrong-numbers)

주어진 숫자의 각 자리의 수를 숫자의 크기만큼 제곱해서 모두 합산 한 후 해당 숫자와 동일한지를 구현하는 실습 과제다.

* 153 : 1^3 + 5^3 + 3^3 = 153 => true
* 1634 : 1^4 + 6^4 + 3^4 + 4^4 = 1634 => true

Gemini의 설명을 참고해 보자!! 😀 [https://g.co/gemini/share/af0a749676aa](https://g.co/gemini/share/af0a749676aa)

**1차 버전**

```rust
// 1차 버전
pub fn is_armstrong_number(num: u32) -> bool {
    let num_str = num.to_string();
    let num_len = num_str.len() as u32;
    let mut sum = 0;
    
    for n in num_str.chars() {
        sum += (n.to_digit(10).unwrap() as u32).pow(num_len); 
    }
    num == sum
}

fn main() {
    assert!(is_armstrong_number(9));
    assert!(is_armstrong_number(153));
    assert!(is_armstrong_number(154));
}
```

**2차 버전**

2차 버전은 이전 [Day_10_Luhn](Day_10_Luhn.md) 구현시 알게된  try_fold()와 map_or()를 사용해 봤다.

```rust
pub fn is_armstrong_number(num: u32) -> bool {
    let len = num.to_string().len() as u32;
	num
	.to_string()
	.chars()
	.try_fold(0, |sum, val| { 
		val.to_digit(10).map(|v| (v.pow(len) + sum)) 
	})
	.map_or(false, |sum| sum == num)
}

fn main() {
    assert!(is_armstrong_number(9));
    assert!(is_armstrong_number(153));
    assert!(is_armstrong_number(154));
}
```

[fold()](https://doc.rust-lang.org/std/iter/trait.Iterator.html#method.fold) 만으로도 충분히 해결할 수 있을 것 같다.

🙏
