```Kotlin
import kotlin.reflect.KProperty  
  
val list = mutableListOf<String>("asdf","asdf")  
  
interface Repository  {  
    fun find() : MutableList<String>  
}  
  
class CrudRepository : Repository {  
    override fun find() : MutableList<String> {  
        return list  
    }  
  
    operator fun getValue(nothing: Nothing?, property: KProperty<*>) =  
         JpaRepository(this)  
}  
  
class JpaRepository(  
    private val crudRepository: CrudRepository  
) : Repository by crudRepository  
  
fun main() = with(System.`in`.bufferedReader()) {  
    val jpaRepository: JpaRepository by CrudRepository()  
  
    print(jpaRepository.find()) //[asdf, asdf]
}
```

어떻게 보면 상속 대신에 쓰일 수도 있는 기능이지만 상속과의 차이점은 상속을 하게 되면 부모 클래스의 구현이 자식 클래스에 드러나지 않는다는 것이다. 특정 기능을 맡기기 위해서 부모 클래스에서는 메서드를 private으로 설정할 수 없다. 이는 결국 캡슐화의 파괴로 이루어지며, 부모 클래스가 변경되면 자식 클래스도 변경되어야 하는 점으로 변경에 유연하지도 못하게 된다.