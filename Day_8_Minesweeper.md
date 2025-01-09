# Minesweep

25년 1월 8일(수)

지뢰찾기 게임을 활용하여 일부 알고리즘을 구현하는 실습을 구현해 봤다. 오늘도 여지없이 혼자 힘으로 완료하지 못하고 Gemini의 힘을 빌렸다. 😂

자세한 실습 내용의 원문은 [이곳](https://exercism.org/tracks/rust/exercises/minesweeper "이곳") 을 참고하면 좋을 것 같다. 요약하자면 3x3, 3x5등의 임의의 2차원 배열 입력값을 주면 입력값을 파싱해서 지뢰 문자(\*)가 있을경우 지뢰의 갯수를 업데이트 해보라는 내용이다.

![[images/Pasted image 20250108185625.png]]

사실 나는 게임을 별로 좋아하지 않아서 지뢰찾기 게임의 알고리즘을 이번에 처음 알게 되었다. 직접 온라인의 지뢰찾기 게임을 해본것도 처음이다. 치매 예방으로 제격이라는 생각이 든다. 😅

위 그림 출력 부분의 숫자는 지뢰의 갯수 이다. 숫자를 기준으로 가로(좌/우), 세로(상/하), 대각선(좌/우 사선) 방향으로 인접해 있는 지뢰 갯수의 합이다.

그러면 이렇게 로직을 구현해보자

- 2중 for문을 사용한다.
- 가로, 세로, 대각선 방향으로 인접해 있는 지뢰를 찾아야 하므로 현재 지점을 기준으로 3x3 영역을 확인한다.
- 다만 세번째 그림처럼 좌표 영역을 벗어나는 경우가 있으므로 로직 구현시 이 부분도 생각해야 한다.

![[images/Pasted image 20250109103819.png]]

최종 구현된 코드는 이렇다. Gemini가 마무리 해줬다. 😀

```rust
pub fn annotate(minefield: &[&str]) -> Vec<String> {
    let rows = minefield.len();
    if rows == 0 {
        return Vec::new();
    }
    let cols = minefield[0].len();

    // with_capacity를 활용해서 메모리 reallocating 방지.
    // https://doc.rust-lang.org/std/vec/struct.Vec.html#method.with_capacity
    let mut annotated_field: Vec<String> = Vec::with_capacity(rows);

    for r in 0..rows {
        let mut annotated_row = String::with_capacity(cols);
        for c in 0..cols {
            if minefield[r].as_bytes()[c] as char == '*' {
                annotated_row.push('*');
                continue;
            }

            let mut count = 0;
            // 3x3 확인 영역 
            // 멋진코드다 👍
            for dr in -1..=1 {
                for dc in -1..=1 {
                    // 현재 중심 위치는 바로 넘어감.
                    if dr == 0 && dc == 0 {
                        continue;
                    }

                    let nr = r as i32 + dr;
                    let nc = c as i32 + dc;
                    // 좌표영역 벗어나는 부분 처리 👍
                    if nr >= 0 && nr < rows as i32 && nc >= 0 && nc < cols as i32 {
                        if minefield[nr as usize].as_bytes()[nc as usize] as char == '*' {
                            // 지뢰 발견하면 갯수 업데이트.
                            count += 1;
                        }
                    }
                }
            }
            if count > 0 {
                // 10진수 숫자를 char형으로 변환후 push
                annotated_row.push(std::char::from_digit(count, 10).unwrap());
            } else {
                annotated_row.push(' ');
            }
        }
        annotated_field.push(annotated_row);
    }

    annotated_field
}

fn main() {
    let (input, expected) = (&[
        "   ",
        " * ",
        "   ",
    ], &[
        "111",
        "1*1",
        "111",
    ]);
    let actual = annotate(input);
    assert_eq!(actual, expected);        
}


```

