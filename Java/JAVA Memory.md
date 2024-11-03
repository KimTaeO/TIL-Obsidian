## Native(off-heap) Memory

Perm Gen : JVM 어플리케이션에서 사용되는 클래스와 메서드들의 메타데이터를 가지고 있다.
자바 8 이전에 사용되었고, 애플리케이션 런 타임에 할당되었으며, Heap 메모리 영역 안에 존재하여 Major GC 발생 시 메모리가 회수되었다.

Metaspace : Perm Gen과 역할은 같으나 Heap 영역 밖(off-heap, Native memory)에 존재하며, 항상 고정된 크기를 가지는 Perm Gen과 달리 크기가 OS가 허용하는 한도까지 자동적으로 증가한다. 클래스 로더와 생명주기가 같도록 설계되어 있다. 

