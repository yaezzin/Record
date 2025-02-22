## equals와 hasCode란 무엇인가?

hasCode와 equals 모두 Object 클래스의 메서드이므로, Object 클래스에서는 기본적으로 **인스턴스의 메모리 주소를 비교**

1. hasCode() 메서드는 그 주소값을 해쉬함수를 통해 Integer의 해쉬값으로 변환하여 비교
2. equals()는 인스턴스의 주소값으로 비교

→ 즉, 모든 객체는 생성되면 서로 전부 다른 객체로 인식함. (하지만 equals()는 객체의 내용이 같은지 비교하는 메서드로 두 객체가 내용상 동일하면 true를 반환해야함)

## 📍 hascode의 존재 이유

equals 메서드로 모든 객체를 비교할 수 있지만 hascode 메서드를 통해 비교를 할까?
그 이유는 equals가 오버라이딩 되어있다는 가정하에 비교를하게 되면 모든 객체들을 하나하나 해당 인스턴스 변수의 값을 비교해주어야함 → 즉 상대적으로 많은 비용이 들어감. hascode를 사용하면 Integer값만 비교하면 되니까!


## 📍 서로의 관계

**1 ) 동일한 객체는 동일한 해시코드를 반환**

- equals()가 true라면 두 객체는 동일한 해시코드 값을 반환함

**2 ) hashCode가 동일하다고 해서 equals()가 반드시 true인 것은 아님**

- **두 객체의 해시코드값이 동등하다고 해서, 객체까지 동등하다고 보장되지는 않음**
    - 해시코드의 값은 범위가 한정적 → 따라서 다른 객체라고 해도 해시코드가 동일할 수 있음 → 해시충돌
- 하지만 서로 다르면 두 객체는 절대로 동등하지 않음

해시코드가 같음? → Yes → equals()도 같음 → 동등한 객체

해시코드가 다름 → No → equals 비교조차 하지않고 서로 다른 객체임!

## 그럼 왜 오버라이딩을 같이 해야하지?

**case 1 ) 둘 다 오버라이딩을 안하는 경우**

두 메서드 모두 해당 객체의 주소값을 이용 (즉, 기본 구현을 사용)

- hasCode()는 해당 객체의 주소값을 기반으로 해쉬값을 생성
- equals()는 메모리 주소 자체를 비교 → 두 객체가 메모리 주소를 참조하는지만 비교

→ 객체 안의 인스턴스 변수들이 같다해도 다른 객체로 간주됨

**case 2 ) equals()만 오버라이딩**

equals()는 객체의 내용을 비교하고, hascode()는 메모리 주소를 기반으로 해시값을 생성

- hascode는 여전히 주소값을 사용하기 때문에, 동등한 객체라도 다른 해시값을 가질 수 있게 됨
- hasCode()가 다르면 HashSet이나 HashMap같은 컬렉션에서 예상치못한 동작 발생가능

**case 3 ) hascode만 오버라이딩 할 경우**

hasCode()가 내용 기반으로 변경되면 동일한 내용의 객체들이 동일한 해시값을 가질 수 있지만, equals()가 여전히 주소값 비교를 하므로 동일한 객체들을 서로 다르다고 인식함


## 결론

hashCode()만 오버라이딩하거나, equals()만 오버라이딩하는 경우 일관성이 깨지므로, 둘 다 오버라이딩하는 것이 안전
