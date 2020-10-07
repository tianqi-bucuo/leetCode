为网站实现一个负载均衡器，提供如下的 3 个功能：

- 添加一台新的服务器到整个集群中 => add(server_id)。
- 从集群中删除一个服务器 => remove(server_id)。
- 在集群中随机（等概率）选择一个有效的服务器 => pick()。
最开始时，集群中一台服务器都没有。每次 pick() 调用你需要在集群中随机返回一个 server_id。

***

一种可行的思路是同时使用哈希表和数组.

- pick(): 数组中随机选取一个元素可以直接使用随机函数得到一个 [0, 数组大小-1] 的整数即可.
- add(server_id): 在数组末尾添加这个server_id, 并在哈希表中添加 server_id -> 数组下标 的键值映射
- remove(server_id): 利用哈希表得到 server_id 的数组下标, 在数组中将它和最末尾的元素交换位置, 然后删除, 并将修改同步到哈希表

```Java
class LoadBalancer {

    private Map<Integer, Integer> dict = null;
    private List<Integer> servers = null;

    public LoadBalancer() {
        // Initialize your data structure here.
        dict = new HashMap<Integer, Integer>();
        servers = new ArrayList<Integer>();
    }

    // @param server_id add a new server to the cluster 
    // @return void
    public void add(int server_id) {
        // Write your code here
        int m = servers.size();
        dict.put(server_id, m);
        servers.add(server_id);
    }

    // @param server_id server_id remove a bad server from the cluster
    // @return void
    public void remove(int server_id) {
        // Write your code here
        int index = dict.get(server_id);
        int m = servers.size();
        dict.put(servers.get(m - 1), index);
        servers.set(index, servers.get(m - 1));
        servers.remove(m - 1);
        dict.remove(server_id);
    }

    // @return pick a server in the cluster randomly with equal probability
    public int pick() {
        // Write your code here
        Random r = new Random();
        int m = servers.size();
        int index = Math.abs(r.nextInt()) % m;
        return servers.get(index);
    } 
}
```