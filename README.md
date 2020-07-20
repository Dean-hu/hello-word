#include<bits/stdc++.h>
using namespace std;
const int inf=2147483647;
struct edge
{
    int to;
    int cost;
};
vector<edge> g[100001];
struct sa
{
    int num;
    int dis;
};
bool operator <(const sa &a,const sa &b)
{
    return a.dis>b.dis;
}
priority_queue<sa> v;
int dv[100001];
int main()
{
    ios::sync_with_stdio(false);
    int n,m,s,x,y,d;
    cin>>n>>m>>s;
    edge tmp;
    sa tmp1;
    for(int i=1; i<=m; i++)
    {
        cin>>x>>y>>d;
        tmp.to=y;
        tmp.cost=d;
        g[x].push_back(tmp);
    }
    fill(dv,dv+n,inf);
    for(int i=1; i<=n; i++)
        dv[i]=inf;
    dv[s]=0;
    tmp1.num=s;
    tmp1.dis=0;
    v.push(tmp1);
    while(!v.empty())
    {
        sa en=v.top();
        v.pop(); //int cd=en.dis;
        int id=en.num;
        for(int i=0; i<g[id].size(); i++)
        {
            edge e1=g[id][i];
            if (dv[id]+e1.cost<dv[e1.to])
            {
                dv[e1.to]=dv[id]+e1.cost;
                tmp1.dis=dv[e1.to];
                tmp1.num=e1.to;
                v.push(tmp1);
            }
        }
    }
    for(int i=1; i<=n; i++)
        cout<<dv[i]<<" "; //cout<<div[n]<<endl;
    return 0;
}
