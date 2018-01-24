#include <cstdio>
#include <algorithm>
using namespace std;
const int maxn=1010;
int hl[maxn]={0};
int father[maxn];
int clusterRoot[maxn]={0};
int rootCount=0;
void init(){
	for(int i=0;i<maxn;i++){
		father[i]=-1;
	}
}
int findroot(int x){
	if(father[x]==-1)return x;
	else{
		father[x]=findroot(father[x]);
		return father[x];
	}
}
void Union(int a, int b){
	int ra=findroot(a);
	int rb=findroot(b);
	if(ra!=rb){
		father[ra]=rb;
	}
}
bool cmp(int a,int b){
	return a>b;
}
int main(int argc, char *argv[])
{
	init();
	int n;
	scanf("%d",&n);
	for(int i=1;i<=n;i++){
		int k;
		scanf("%d:",&k);
		for(int j=0;j<k;j++){
			int hno;
			scanf("%d",&hno);
			if(hl[hno]==0){
				hl[hno]=i;
			}else{
				Union(i,hl[hno]);
			}
		}
	}
	for(int i=1;i<=n;i++){
		int root=findroot(i);
		if(clusterRoot[root]==0)rootCount++;
		clusterRoot[root]++;
	}
	sort(clusterRoot+1,clusterRoot+n+1,cmp);
	printf("%d\n",rootCount);
	for(int i=1;i<=rootCount;i++){
		printf("%d",clusterRoot[i]);
		if(i!=rootCount)printf(" ");
	}
	return 0;
}
