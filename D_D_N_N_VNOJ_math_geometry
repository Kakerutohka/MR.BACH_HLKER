#include <bits/stdc++.h>
using namespace std;
typedef pair<double, int> ii;
int Lx, Ly, Rx, Ry;
int n, idx, cheo[1011][1011];
double sx, sy, ex, ey;
double d[80001];
struct Canh // được cấu thành từ 2 điểm => có 2 tọa độ
{
    double lx, ly, rx, ry;
};
Canh edge[80001];
struct Dinh // được cấu thành từ 1 điểm và có 2 tọa độ là x và y
{
    double x, y;
};
Dinh node[80001];
vector <pair<double, int> > g[80001];

long long areatri(Dinh A, Dinh B, Dinh C)
{
    long long x = (B.x-A.x)*(B.y+A.y) + (C.x-B.x)*(C.y+B.y) + (A.x-C.x)*(A.y+C.y);
    return x;

}

void TaoDuongDiKhongCat()
{
    //với mỗi 2 đỉnh bất kì thì check xem nó có cắt cạnh nào của hình chữ nhật không, nếu không cắt thì thêm vào đồ thị
    for (int i=1; i<=idx+2; i++)
    {
        for (int j=i+1; j<=idx+2; j++)
        {
            if (cheo[i][j]==0)
            {
                int flag = 0;
                for (int k=1; k<=idx; k++)
                {
                    Dinh X, Y;
                    X.x = edge[k].lx;
                    X.y = edge[k].ly;
                    Y.x = edge[k].rx;
                    Y.y = edge[k].ry;
                    if ((areatri(X,Y,node[i])*areatri(X,Y,node[j]))<0 && (areatri(node[i], node[j], X)*areatri(node[i], node[j], Y))<0)
                    {
                        flag = 1;
                        break;
                    }
                }
                if (flag==0)
                {

                    double distanc = sqrt((node[j].x-node[i].x)*(node[j].x-node[i].x)+(node[j].y-node[i].y)*(node[j].y-node[i].y));
                    //cout<<i<<" "<<node[i].x<<" "<<node[i].y<<" "<<j<<endl;
                    g[i].push_back({distanc, j});
                    g[j].push_back({distanc, i});
                }
            }
        }
    }
}
void dijkstra(int u)
{
    priority_queue <ii, vector <ii>, greater<ii> > pq;
    for (int i=1; i<=idx+2; i++)
    {
        d[i] =1e9;
    }
    d[u]=0;
    pq.push({0, u});
    while (pq.size())
    {
        int u = pq.top().second;
        double du = pq.top().first;
        pq.pop();
        if (du!=d[u]) continue;
        for (int i=0; i<g[u].size(); i++)
        {
            int v = g[u][i].second;
            double uv = g[u][i].first;
            if (d[v]>du+uv)
            {
                d[v] = du + uv;
                pq.push({d[v], v});
            }
        }
    }

}
int main()
{
  ios_base::sync_with_stdio(0);
    cin.tie(0);
    cout.tie(0);
    cin>>n;
    cin>>sx>>sy;
    cin>>ex>>ey;
    for (int i=1; i<=n; i++)
    {
        cin>>Lx>>Ly>>Rx>>Ry;

        //canh tren
        idx++;
        edge[idx].lx = Lx;
        edge[idx].ly = Ly;
        edge[idx].rx = Rx;
        edge[idx].ry = Ly;
        //điểm có thứ tự:
        node[idx].x = Lx;
        node[idx].y = Ly;

        //canh phai
        idx++;
        edge[idx].lx = Rx;
        edge[idx].ly = Ly;
        edge[idx].rx = Rx;
        edge[idx].ry = Ry;
        //điểm có thứ tự:
        node[idx].x = Rx;
        node[idx].y = Ly;

        //canh duoi
        idx++;
        edge[idx].lx = Lx;
        edge[idx].ly = Ry;
        edge[idx].rx = Rx;
        edge[idx].ry = Ry;
        //điểm có thứ tự:
        node[idx].x = Rx;
        node[idx].y = Ry;

        //canh trai
        idx++;
        edge[idx].lx = Lx;
        edge[idx].ly = Ly;
        edge[idx].rx = Lx;
        edge[idx].ry = Ry;
        //điểm có thứ tự:
        node[idx].x = Lx;
        node[idx].y = Ry;

        //thứ tự đỉnh  tạo thành đường chéo
        cheo[idx][idx-2] = 1;
        cheo[idx-2][idx] = 1;
        cheo[idx-1][idx-3] = 1;
        cheo[idx-3][idx-1] = 1;
    }
    //thêm 2 đỉnh bắt đầu và kết thúc
    node[idx+1].x = sx;
    node[idx+1].y = sy;
    node[idx+2].x = ex;
    node[idx+2].y = ey;
    TaoDuongDiKhongCat();
    dijkstra(idx+1);
    cout<<setprecision(3)<<fixed<<d[idx+2];

}
