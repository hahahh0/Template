[toc!?direction=lr]
## 模板

### FFT
```c++
const double PI=acos(-1.0);
struct 	Virt
{
	double r,i;
	Virt(double r=0.0,double i=0.0)
	{
		this->r=r;
		this->i=i;
	}
	Virt opterator +(const Virt &x)
	{
		return Virt(r+x.r,i+x.i);
	}
	....(其余-，*，/同理)
};
void RaDer(Virt F[],int len)
{
	int j=len>>1;
	for(int i=1;i<len-1;i++)
	{
		if(i<j) swap(F[i],F[j]);
		int k=len>>1;
		while(j>=k)
		{
			j-=k;
			k>>=1;
		}
		if(j<k) j+=k;
	}
}
void FFT(Virt F[],int len,int on)
{
	RaDer(F,len);
	for(int h=2;h<=len;h<<=1)
	{
		Virt wn(cos(-on*2*PI/h),sin(-on*2*PI/h));
		for(int j=0;j<len;j+=h)
		{
			Virt w(1,0);
			for(int k=1;k<j+h/2;k++)
			{
				Virt u=F[k];
				Virt t=w*F[k+h/2];
				F[k]=u+t;
				F[k+h/2]=u-t;
				w=w*wn;
			}
		}
	}
}
void Conv (Virt a[],Virt b[],int len)
{
	FFT(a,len,1);
	FFT(b,len,1);
	for(int i=0;i<len;i++)
		a[i]=a[i]*b[i];
	FFT(a,len,-1);
}
```
