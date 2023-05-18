###모든 자료의 출처는 Chat GPT입니다.
1. 정규 표현식 (Regular Expression)

-정규 표현식이란 Python에서 패턴의 일치 및 텍스트 조작을 위한 강력한 도구로써 정규 표현식을 위한 re라는 내장 모듈을 있습니다.
 정규 표현식을 사용하기 위해 사용되는 함수와 메소드 등이 있습니다


    -함수
        1.re.match(pattern, string)
            문자열의 시작 부분의 패턴을 일치시키며, 패턴이 일치할 경우 일치 객체를 반환하며, 아닐 경우 NONE을 반환합니다.
            >>> m = p.match("python")
            >>> print(m)
            <re.Match object; span=(0, 6), match='python'>
            p = re.compile(정규표현식)
            m = p.match('string goes here')
            if m:
                print('Match found: ', m.group())
            else:
                print('No match')


        2.re.search(pattern, string)   
            패턴과 일치하는  문자열을 검색하며 일치할 경우 객체를 반환하며, 아닐 경우 NONE을 반환합니다.
            >>> m = p.search("3 python")
            >>> print(m)
            <re.Match object; span=(2, 8), match='python'>

        3.re.findall(pattern, string)
            패턴이 겹치지 않는 모든 일치 항목의 문자역 목록(List)를 반환합니다.
            >>> result = p.findall("life is too short")
            >>> print(result)
            ['life', 'is', 'too', 'short']


        4.re.finditer(pattern, string)
            문자열에서 패턴이 겹치지 않는 모든 일치 항목에 댛해서 일치 객체를 반환하는 반복자를 반환합니다.
            >>> result = p.finditer("life is too short")
            >>> print(result)
            <callable_iterator object at 0x01F5E390>
            >>> for r in result: print(r)
            ...
            <re.Match object; span=(0, 4), match='life'>
            <re.Match object; span=(5, 7), match='is'>
            <re.Match object; span=(8, 11), match='too'>
            <re.Match object; span=(12, 17), match='short'>    
                    
        5.re.sub(pattern, repl, string)
            문자열에서 패턴(pattern)으로 지정된 모든 항목을  repl에 지정된 문자열로 바꿉니다.

    
    -메소드
       1. .(점): 새 줄을 제외한 모든 문자와 일치합니다.

       2. *(별표): 이전 문자 또는 그룹의 0개 이상의 발생과 일치합니다.

       3. +(더하기): 이전 문자 또는 그룹의 하나 이상의 항목과 일치합니다.

       4. ?(물음표): 이전 문자 또는 그룹의 0개 또는 1개 항목과 일치합니다.

       5. \d: 모든 숫자 문자(0-9)와 일치합니다.

       6. \w: ??모든 영숫자 문자(a-z, A-Z, 0-9 및 밑줄)와 일치합니다.

       7. []: 괄호 안의 단일 문자와 일치합니다.

       8. |(파이프): 파이프 앞이나 뒤의 표현식과 일치합니다.




2. 가비지 컬렉션 (Garbage Collection)
- 프로그램 내부에서 더 이상 사용하지 않는 메모리를 자동으로 식별 회수하는 컴퓨터 프로그래밍 프로세스 입니다. 이는 메모리 리소스의 효율적인 관리를 위해 사용하며,
  자동 메모리 관리를 사용하는 Python, Java, C#과 같은 프로그래밍 언어의 경우 중요한 역할을 수행하며 동적으로 메모리를 할당하고, 메모리 할당 헤제의 경우
  가비지 수집기에 의해 처리합니다.

  가비지 수집기(garbage collector)의 경우 프로그램 내부에서 더이상 엑세스하거나 참조할 수없는 메모리 객체를 식별하여 작동하며, 더 이상 필요 없는 객체를 결정하고,
  해당 객체가 차지하는 메모리를 해제하여 나중에 다시 사용할 수 있도록 한다.

- 수행 순서 
    1. 표시
        가비지 수집기는 알려진 루트 객체(ex)전역 변수, 지역 변수 및 활성 스레드) 에서 시작하여 객체 그래프를 순회하고 루트에서 도달할 수 있는 모든 객체를 파악한다.

    2. 스웝
        도달 가능한 객체를 표시한 후 전체 메모리 공간을 파악하고, 도달할 수 없는 객체가 차지하는 메모리를 식별하고 해체합니다.

    3. 압축
        일부 가비지 컬렉션 중에서 압축이라는 추가적인 단계를 수행하는데 접근 가능한 객체를 메모리에서 더 가깝게 이동하여 조각화를 줄이고 메모리 사용을 최적화하는 작업을 수행한다.




- GC 가 제대로 동작되도록 코드를 어떻게 작성해야 하는지, 어떻게 하면 GC 로도 메모리 leak 이 발생되는지 예제 코드와 함께 설명
 
- 자동 GC
import gc

print "Garbage collection thresholds: %r" % gc.get_threshold()



> Garbage collection thresholds: (700, 10, 10)

시스템의 기본 한계치 값은 700인것을 확인할 수 있다. 메모리 할당과 해제를 비교해서 700 이상이라면 GC가 실행될수 있다는 것을 의미한다.


- 수동 GC
    import sys, gc



    def maek_cycle():

        l = { }

        l[0] = l



    def main():

        collected = gc.collect()

        print (collected)

        for i in range(10):

            make_cycle()

        collected = gc.collect()

        print(collected)



    if __name__ == "__main__":

        ret = main()

        sys.exit(ret)


- GC 로드 메모리 Leak란?
    - 메모리 누수란? 더이상 사용하지 않는 객체가 GC에 의해 회수 되지 않고, 계속 누적되는 현상을의미 하며 Old영역에 누적된 객체로 인하여 GC가 빈번하게 작동하여, 프로그램의
      응답속도가 늦어지며 결국 OOM(Out Of Memory)오류로 종료를 유발하게 된다.

      JAVA의 경우 발생하는 원인은 

        1. Integer, Long 같은 래퍼 클래스를 이용하여, 무의미한 객체를 생성하는 경우
            public class Adder {
                publiclong addIncremental(long l)
                {
                        Long sum=0L;
                        sum =sum+l;
                        return sum;
                }
                public static void main(String[] args) {
                        Adder adder = new Adder();
                        for(long ;i<1000;i++)
                        {
                                adder.addIncremental(i);
                        }
                }
            }


        2. Map에 캐쉬 데이터를 선언하고 해제하지 않는 경우
            import java.util.HashMap;
            import java.util.Map;
                public class Cache {
                    private Map<String,String> map= new HashMap<String,String>();
                    publicvoid initCache()
                    {
                            map.put("Anil", "Work as Engineer");
                            map.put("Shamik", "Work as Java Engineer");
                            map.put("Ram", "Work as Doctor");
                    }
                    public Map<String,String> getCache()
                    {
                            return map;
                    }
                    publicvoid forEachDisplay()
                    {
                            for(String key : map.keySet())
                            {
                                String val = map.get(key);                 
                                System.out.println(key + " :: "+ val);
                            }
                    }
                    public static void main(String[] args) {            
                            Cache cache = new Cache();
                            cache.initCache();
                            cache.forEachDisplay();
                    }
                }


        3. 스트림 객체를 사용하고 닫지 않는 경우
            try{
                Connection con = DriverManager.getConnection();
                …………………..
                    con.close();
                }

                Catch(exception ex)
                {
            }


        4. Map의 키를 사용자 객체로 정의하면서 equals(), hascode()를 재정의 하지 않아서 같은 키로 착각하여 데이터가 계속 쌓이게 되는 경우
            import java.util.HashMap;
            import java.util.Map;

            public class CustomKey {
                public CustomKey(String name)
                {
                        this.name=name;
                }
                
                private String name;
                
                publicstaticvoid main(String[] args) {
                        Map<CustomKey,String> map = new HashMap<CustomKey,String>();
                        map.put(new CustomKey("Shamik"), "Shamik Mitra");
                        String val = map.get(new CustomKey("Shamik"));
                        System.out.println("Missing equals and hascode so value is not accessible from Map " + val);
                }
            }


        5. Map의 키를 사용자 객체로 정의하면서 equals(), hashcode()를 재정의 하였지만, 키값이 불편 데이터가 아니라서 데이터 비교시 계속 변하는 경우
            import java.util.HashMap;
            import java.util.Map;

            public class MutableCustomKey {
                public MutableCustomKey(String name) {
                    this.name = name;
                }

                private String name;

                public String getName() {
                    return name;
                }

                public void setName(String name) {
                    this.name = name;
                }

                @Override
                public int hashCode() {
                    final int prime = 31;
                    int result = 1;
                    result = prime * result + ((name == null) ? 0 : name.hashCode());
                    return result;
                }

                @Override
                public boolean equals(Object obj) {
                    if (this == obj)
                        return true;
                    if (obj == null)
                        return false;
                    if (getClass() != obj.getClass())
                        return false;
                    MutableCustomKey other = (MutableCustomKey) obj;
                    if (name == null) {
                        if (other.name != null)
                            return false;
                    } else if (!name.equals(other.name))
                        return false;
                    return true;
                }

                public static void main(String[] args) {
                    MutableCustomKey key = new MutableCustomKey("Shamik");
                    Map<MutableCustomKey, String> map = new HashMap<MutableCustomKey, String>();
                    map.put(key, "Shamik Mitra");
                    MutableCustomKey refKey = new MutableCustomKey("Shamik");
                    String val = map.get(refKey);
                    System.out.println("Value Found " + val);
                    key.setName("Bubun");
                    String val1 = map.get(refKey);
                    System.out.println("Due to MutableKey value not found " + val1);
                }
            }


        6. 자료구조를 생성하여 사용하면서, 구현 오류로 인해 메모리를 해제하지 않는 경우 
            public class Stack {

            privateint maxSize;
            privateint[] stackArray;
            privateint pointer;
            
            public Stack(int s) {
                    maxSize = s;
                    stackArray = newint[maxSize];
                    pointer = -1;
            }
            
            public void push(int j) {
                    stackArray[++pointer] = j;
            }
            
            public int pop() {
                    return stackArray[pointer--];
            }
            
            public int peek() {
                    return stackArray[pointer];
            }
            
            publicboolean isEmpty() {
                    return (pointer == -1);
            }
            
            public boolean isFull() {
                    return (pointer == maxSize - 1);
            }
            
            public static void main(String[] args) {
            
                    Stack stack = new Stack(1000);
                    
                    for(int i = 0; i<1000; i++) {
                            stack.push(i);
                    }
                    
                    for(int i = 0; i<1000; i++) {
                            int element = stack.pop();
                            System.out.println("Poped element is "+ element);
                    }
            }
        }
