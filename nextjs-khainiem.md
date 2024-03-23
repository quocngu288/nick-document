## Pre-Rendering

- Render sắn file html trên server (User start lên đã có sắn file html rồi, nhưng chưa có event). Sau đó tiếp tục thực hiện quá trình Hydration, load file javascript lên -> thực hiện được event

## No Rerendering

- Ban đầu khởi tạo 1 trang trắng. Sau đó tiếp tục thực hiện quá trình Hydration

## SSG - Static-Site-Generation

- Build sẵn file HTML. User request sẽ trả về liền (Build time)

```js
import { GetStaticProps, GetStaticPropsContext } from "next";

interface PostList {
  post: any[];
}

export default function index(props: PostList) {
  return <div>Day là list post</div>;
}

// hàm này sẽ được gọi 1 lan khi build ở môi trương Production
// ở môi trương dev thì hàm này luôn được gọi lại mỗi request
export const getStaticProps: GetStaticProps<PostList> = async (
  context: GetStaticPropsContext
) => {
  return {
    props: {
      post: [],
    },
  };
};
```

## SSG - Server-Site-Rendering

- Theo mỗi request sẻ tạp 1 file HTML trả về (Run time)

## CSG - Client-Site-Rendering

-

## ISR - Increamental-Static-Regeneration

-

## Automatic static Optimization (ASO)

- Next js dựa bào GetServerSideProps hoặc GetInitialProps trong page để xác đinh trang đó có Static hay không (có thể rerender được hay không). Nó sẽ bật mode ASO

- Nếu đang ASO thì khi buil, ouput file sẽ là file HTML. Còn Not ASO, thì file ouput sẽ là file js
