tanstack-query에서 *staleTime* 과 *gcTime* 은 데이터를 캐싱하고 관리하는 데 중요한 두 가지 설정 값이다.  
요약하면 *staleTime* 은 데이터가 얼마나 오래 '신성한 상태'로 유지되는지를 정하는 시간이고, *gcTime* 은 해당 쿼리를 사용하는 곳이 없게 된 이후에도 캐시 데이터를 얼마 동안 유지할지를 정하는 시간이다.

먼저, staleTime은 데이터를 처음 가져온 후에 그 데이터를 '신성한' 상태로 간주하는 시간을 말한다. staleTime 내에는 같은 쿼리에 대한 새로운 네트워크 요청이 일어나지 않고, 캐시 데이터를 그대로 사용하게 된다.  
예를 들어, staleTime을 5분으로 설정하면, 데이터를 가져오고 나서 5분 동안은 이 데이터가 '신선하다'고 판단해서 쿼리 호출 시 추가 네트워크 요청 없이 캐시 데이터를 계속 사용한다.  
그리고 staleTime이 지난 후 해당 쿼리를 호출한다면 새로운 요청을 보내 데이터를 갱신하게 된다.  
이 때 staleTime의 기본값은 0이다.

반면에 gcTime은 해당 쿼리가 더 이상 사용되지 않을 때, 캐시 데이터가 메모리에 얼마나 더 남아있을지를 정하는 시간이다.  
staleTime이 지나면 데이터는 '오래된' 상태가 되지만, 여전히 캐시된 데이터는 사용이 가능하다.  
이 캐시 데이터는 새로운 요청을 보내 신선한 데이터를 받아오기 이전에 임시로 기존 데이터를 표시하는데 활용된다.  

staleTime은 데이터를 처음 가져온 후 얼마 동안 네트워크 요청 없이 캐시된 데이터를 사용할지를 정하는 시간이고,  
gcTime은 해당 쿼리가 사용되지 않게 된 후에도 캐시에 유지될 시간을 정하는 것이다.  
이렇게 각각의 설정을 통해 데이터를 더 효율적으로 관리하고, 불필요한 네트워크 요청을 줄이면서도 최신 데이터를 가져올 수 있도록 한다.

----
- [[tanstack-query 공식문서] caching example](https://tanstack.com/query/v5/docs/framework/react/guides/caching)
- [[tanstack-query 공식문서] staleTime property](https://tanstack.com/router/latest/docs/framework/react/api/router/RouteOptionsType#staletime-property)
