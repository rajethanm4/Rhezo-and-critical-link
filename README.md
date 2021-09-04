# Rhezo-and-critical-link
#include <bits/stdc++.h>
#define IOS                  \
	ios::sync_with_stdio(0); \
	cin.tie(0);              \
	cout.tie(0);
#define endl "\n"
#define int long long
#define pb push_back
#define mp make_pair
#define f1(i, a, b) for (int i = a; i < b; i++)
#define f2(i, a, b) for (int i = a; i > b; i--)
#define ff first
#define ss second
#define lb lower_bound
#define ub upper_bound
#define mod 1000000007
#define pq priority_queue<int,vector<int>,greater<int> > //for min heap.
using namespace std;
vector<int> arr[100002];
bool vis[100002];
int par[100002];
int inr[100002],low[100002];
int siz[100002];
int n,m,p,u,v,x;
int cnt,timer=1;
void find_size(int node,int par=0)
{
	vis[node]=1;
	for(int child : arr[node])
	{
		if(!vis[child])
		{
			find_size(child,node);
			 siz[node]+=siz[child];
		}
	}
	siz[node]+=1;
}
void dfs(int node)
{
  vis[node]=true;
  inr[node] = low[node] = timer++;
  for(int child: arr[node])
  {
    if(!vis[child]){
    par[child]=node;
    dfs(child);
    low[node]=min(low[node],low[child]);
     if((low[child]>inr[node]) && (p>abs(x-2*siz[child])))
     {
		cnt++;			 
     } 
    }
     else if(child != par[node]){
     low[node]=min(low[node],inr[child]);
    }
  }
}
int32_t main()
{    IOS;
	cin>>n>>m>>p;
	while(m--)
	{
		cin>>u>>v;
		arr[u].pb(v);
		arr[v].pb(u);
	}
	f1(i,1,n+1)
	 {
	 	if(!vis[i])
		   {
		   	find_size(i);
		   }
	   }
	   memset(vis,false,sizeof(vis));
	   memset(inr,false,sizeof(inr));
	   memset(low,false,sizeof(low));
	f1(i,1,n+1)
	  {
	  	if(!vis[i]){ 
	  	 x=siz[i];
	  	 dfs(i);
	  	}
	  }
	cout<<cnt<<endl;
}
