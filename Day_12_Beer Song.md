# 🍺 Beer Song

25년 1월 13일(월) ☔️⛇

https://exercism.org/tracks/rust/exercises/beer-song

주어진 값으로 반복되는 노래 가사를 제어하는 실습 과제다.

영어에는 단수형, 복수형이 있으니까 그 부분을 가사 반복시 주의해야 했다. 그리고 주어진 값이 0일때는 반복되는 가사 패턴이 달라져서 그 구분도 로직 구현시 처리 해줘야 했다.

	99 bottles, 1 bottle, No more...

verse(n: u32), sing(start: u32, end: u32) 이 두개의 함수를 구현하면 된다. 함수 시그니처를 봤을 때 verse()에서 가사를 제어하면 되고, sing()은 범위값을 인자로 받으니까 loop 안에서 verse()를 호출하는 방법으로 완료하면 된다고 생각했다.

아주 쉬운데 생각했지만 막상 해보면 역시 쉽지가 않다.  완료하고 테스트는 통과 했지만 효율적인 코드는 아닌것 같다.🤔

**내 버전**
```rust
pub fn verse(n: u32) -> String {
    if n > 1 {
        if (n - 1) > 1 {
            format!("{} bottles of beer on the wall, {} bottles of beer.\nTake one down and pass it around, {} bottles of beer on the wall.", n, n, n-1)    
        } else {
            format!("{} bottles of beer on the wall, {} bottles of beer.\nTake one down and pass it around, {} bottle of beer on the wall.", n, n, n-1)    
        }
    } else if n == 1 {
        format!("{} bottle of beer on the wall, {} bottle of beer.\nTake it down and pass it around, no more bottles of beer on the wall.", n, n)
    } else {
        "No more bottles of beer on the wall, no more bottles of beer.\nGo to the store and buy some more, 99 bottles of beer on the wall.".to_string()
    }
}

pub fn sing(start: u32, end: u32) -> String {
    let mut return_string: Vec<String> = Vec::new(); 
    
    for n in (end..=start).rev() {
        return_string.push(verse(n));
        return_string.push("\n\n".to_string());
    }
    return_string.join("")
}

```

sing()이 뭔가 마음에 들지 않고, verse()는 더 마음에 안든다. 그럴때는 커뮤니티 솔루션을 찾아보면 된다. 😅

좋아요가 많은 솔루션은 그럴만한 이유가 있다. 

👍👍강추 버전
- https://exercism.org/tracks/rust/exercises/beer-song/solutions/rutaka-n : 재귀를 사용해서 처리하다니 !! 맙소사. 멋진 코드다. 나도 써보야지!! 
- https://exercism.org/tracks/rust/exercises/beer-song/solutions/bernardoamc : 역쉬 map을 이용해서 한줄로 sing()을 처리하다니 멋지구만 !! 