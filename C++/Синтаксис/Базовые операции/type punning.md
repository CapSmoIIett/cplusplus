#Syntax

[Страничка википедии](https://en.wikipedia.org/wiki/Type_punning)

Любой метод обхода системы типов в языке программирования 

#### Использование указателей 

```c++
uint64_t protocol_id = 0x41727101980;
const uint8_t* protocol_id_bytes = reinterpret_cast<const uint8_t *>(&protocol_id);
msg.insert(msg.end(), protocol_id_bytes, protocol_id_bytes + sizeof(protocol_id));
```


#### Использование union

Это только для С

```c++
bool is_negative ( float x ) 
{ 
    union 
    { 
        int i ; 
        float d ; 
    } my_union;

    my_union.d = x; 
    return my_union.i < 0;  // Сравнение int быстрее чем double 
}   
```

#### Использование bit_cast

```c++
constexpr bool is_negative ( float x ) noexcept 
{ 
    static_assert (std::numeric_limits <float>:: is_iec559 ); // (включено только в IEEE 754) 
    auto i = std::bit_cast<std::int32_t> (x); 
    return i < 0; 
} 
```