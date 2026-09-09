<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:E07A5F,100:3D5A45&height=180&section=header&text=Culinary%20Blog&fontSize=50&fontColor=ffffff&animation=fadeIn&fontAlignY=40&desc=Nền%20tảng%20chia%20sẻ%20và%20khám%20phá%20công%20thức%20nấu%20ăn&descAlignY=62&descSize=18" width="100%"/>

  <p><b>Điểm khởi đầu của dự án</b> — hướng dẫn cài đặt, triển khai và quy ước làm việc</p>

  <a href="https://github.com/PTUDW-2026-Nhom2/CulinaryBlog">
    <img src="https://img.shields.io/badge/Source_Code-CulinaryBlog-24292e?style=for-the-badge&logo=github" />
  </a>
  <a href="https://nestjs.com">
    <img src="https://img.shields.io/badge/NestJS-Backend-E0234E?style=for-the-badge&logo=nestjs&logoColor=white" />
  </a>
  <a href="https://nextjs.org">
    <img src="https://img.shields.io/badge/Next.js-Frontend-000000?style=for-the-badge&logo=next.js&logoColor=white" />
  </a>
  <a href="https://www.postgresql.org">
    <img src="https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" />
  </a>

</div>

<hr/>

<h2>📖 Giới thiệu</h2>

<p><b>Culinary Blog</b> là nền tảng web cho phép người dùng đăng tải, khám phá và tìm kiếm công thức nấu ăn từ nhiều nền ẩm thực. Hệ thống xây dựng theo mô hình <b>API-Driven Architecture</b>, backend áp dụng <b>Clean Architecture</b> kết hợp <b>CQRS</b>, với đầy đủ cơ chế xác thực, tìm kiếm toàn văn tiếng Việt, caching và quan sát hệ thống.</p>

<p>Repo <code>manifest</code> này <b>không chứa source code</b>. Toàn bộ code nằm ở monorepo <a href="https://github.com/PTUDW-2026-Nhom2/CulinaryBlog">CulinaryBlog</a>. Đây là nơi tập trung hướng dẫn triển khai và quy ước làm việc mà mọi thành viên phải tuân thủ.</p>

<h2>🧱 Kiến trúc hệ thống</h2>

<pre><code>┌──────────────────────┐         ┌───────────────────────────┐
│   NEXT.JS FRONTEND   │◄───────►│      NESTJS BACKEND       │
│   App Router :3000   │  REST   │  Clean Arch + CQRS :5000  │
└──────────────────────┘  JSON   └─────────────┬─────────────┘
                                               │
     ┌──────────┬──────────┬──────────┬────────┴─────┬──────────────┐
     │PostgreSQL│  Redis   │  MinIO   │   BullMQ     │ Google OAuth │
     │  :5432   │  :6379   │  :9000   │    Jobs      │     2.0      │
     └──────────┴──────────┴──────────┴──────────────┴──────────────┘</code></pre>

<h2>🛠️ Tech Stack</h2>

<table>
  <thead>
    <tr><th>Thành phần</th><th>Công nghệ</th></tr>
  </thead>
  <tbody>
    <tr><td>Backend</td><td>NestJS (TypeScript) — Clean Architecture + CQRS qua <code>@nestjs/cqrs</code></td></tr>
    <tr><td>Frontend</td><td>Next.js App Router, TypeScript, Tailwind CSS</td></tr>
    <tr><td>Database</td><td>PostgreSQL 16 + Drizzle ORM — Full-Text Search tiếng Việt</td></tr>
    <tr><td>Cache</td><td>Redis 7 (<code>ioredis</code>)</td></tr>
    <tr><td>Object Storage</td><td>MinIO (S3-compatible)</td></tr>
    <tr><td>Background Jobs</td><td>BullMQ</td></tr>
    <tr><td>Xác thực</td><td>JWT (access 15 phút, refresh 7 ngày có rotation) + Google OAuth 2.0</td></tr>
    <tr><td>Validation</td><td><code>class-validator</code> + <code>class-transformer</code></td></tr>
    <tr><td>Observability</td><td>Pino (logging) + OpenTelemetry (tracing)</td></tr>
    <tr><td>Triển khai</td><td>Docker Compose + Nginx reverse proxy</td></tr>
  </tbody>
</table>

<hr/>

<h2>🚀 Cài đặt và chạy dự án</h2>

<h3>Yêu cầu môi trường</h3>

<table>
  <thead>
    <tr><th>Công cụ</th><th>Phiên bản tối thiểu</th></tr>
  </thead>
  <tbody>
    <tr><td>Node.js</td><td>20</td></tr>
    <tr><td>pnpm</td><td>9</td></tr>
    <tr><td>Docker + Docker Compose</td><td>Bản mới nhất</td></tr>
    <tr><td>Git</td><td>2.40</td></tr>
  </tbody>
</table>

<h3>Bước 1 — Clone source code</h3>

<pre><code>git clone https://github.com/PTUDW-2026-Nhom2/CulinaryBlog.git
cd CulinaryBlog</code></pre>

<h3>Bước 2 — Cài pnpm</h3>

<pre><code>corepack enable
corepack prepare pnpm@9.12.0 --activate</code></pre>

<h3>Bước 3 — Cấu hình biến môi trường</h3>

<pre><code>cp .env.example .env</code></pre>

<p>Mở <code>.env</code> và điền các biến bắt buộc:</p>

<table>
  <thead>
    <tr><th>Biến</th><th>Mô tả</th></tr>
  </thead>
  <tbody>
    <tr><td><code>JWT_ACCESS_SECRET</code></td><td>Chuỗi bí mật ký access token</td></tr>
    <tr><td><code>JWT_REFRESH_SECRET</code></td><td>Chuỗi bí mật ký refresh token</td></tr>
    <tr><td><code>GOOGLE_CLIENT_ID</code></td><td>Lấy từ Google Cloud Console</td></tr>
    <tr><td><code>GOOGLE_CLIENT_SECRET</code></td><td>Lấy từ Google Cloud Console</td></tr>
  </tbody>
</table>

<p>⚠️ <b>Tuyệt đối không commit file <code>.env</code> lên Git.</b></p>

<h3>Bước 4 — Cài dependencies</h3>

<pre><code>pnpm install</code></pre>

<h3>Bước 5 — Khởi động hạ tầng</h3>

<pre><code>docker compose up -d postgres redis minio</code></pre>

<h3>Bước 6 — Chạy migration</h3>

<pre><code>pnpm db:migrate</code></pre>

<h3>Bước 7 — Chạy dự án</h3>

<pre><code>pnpm dev</code></pre>

<table>
  <thead>
    <tr><th>Service</th><th>URL</th></tr>
  </thead>
  <tbody>
    <tr><td>Frontend</td><td><code>http://localhost:3000</code></td></tr>
    <tr><td>Backend API</td><td><code>http://localhost:5000/api/v1</code></td></tr>
    <tr><td>API Docs (Scalar)</td><td><code>http://localhost:5000/scalar</code></td></tr>
    <tr><td>MinIO Console</td><td><code>http://localhost:9001</code></td></tr>
  </tbody>
</table>

<h3>Chạy toàn bộ bằng Docker</h3>

<pre><code>docker compose up --build</code></pre>

<h3>Các lệnh thường dùng</h3>

<table>
  <thead>
    <tr><th>Lệnh</th><th>Chức năng</th></tr>
  </thead>
  <tbody>
    <tr><td><code>pnpm dev</code></td><td>Chạy song song backend và frontend</td></tr>
    <tr><td><code>pnpm dev:be</code></td><td>Chỉ chạy backend</td></tr>
    <tr><td><code>pnpm dev:fe</code></td><td>Chỉ chạy frontend</td></tr>
    <tr><td><code>pnpm lint</code></td><td>Kiểm tra lint toàn workspace</td></tr>
    <tr><td><code>pnpm typecheck</code></td><td>Kiểm tra kiểu TypeScript</td></tr>
    <tr><td><code>pnpm db:generate</code></td><td>Sinh migration từ schema Drizzle</td></tr>
    <tr><td><code>pnpm db:migrate</code></td><td>Áp dụng migration vào database</td></tr>
  </tbody>
</table>

<hr/>

<h2>📝 Quy ước Commit</h2>

<p>Nhóm áp dụng chuẩn <b>Conventional Commits</b>. Mọi commit bắt buộc theo định dạng:</p>

<pre><code>&lt;type&gt;(&lt;scope&gt;): &lt;mô tả ngắn&gt;</code></pre>

<h3>Danh sách type</h3>

<table>
  <thead>
    <tr><th>Type</th><th>Dùng khi</th><th>Ví dụ</th></tr>
  </thead>
  <tbody>
    <tr><td><code>feat</code></td><td>Thêm tính năng mới</td><td><code>feat(recipes): thêm api tạo công thức</code></td></tr>
    <tr><td><code>fix</code></td><td>Sửa lỗi</td><td><code>fix(auth): sửa lỗi refresh token bị revoke sớm</code></td></tr>
    <tr><td><code>chore</code></td><td>Việc lặt vặt, không đổi logic</td><td><code>chore(deps): cập nhật drizzle-orm lên 0.33</code></td></tr>
    <tr><td><code>docs</code></td><td>Sửa tài liệu, README</td><td><code>docs(readme): bổ sung hướng dẫn cài minio</code></td></tr>
    <tr><td><code>style</code></td><td>Format code, không đổi logic</td><td><code>style(frontend): format lại theo prettier</code></td></tr>
    <tr><td><code>refactor</code></td><td>Sửa cấu trúc, không thêm tính năng</td><td><code>refactor(categories): tách query handler</code></td></tr>
    <tr><td><code>perf</code></td><td>Tối ưu hiệu năng</td><td><code>perf(search): thêm index cho tsvector</code></td></tr>
    <tr><td><code>test</code></td><td>Thêm hoặc sửa test</td><td><code>test(auth): thêm unit test cho login handler</code></td></tr>
    <tr><td><code>build</code></td><td>Sửa Dockerfile, cấu hình build</td><td><code>build(docker): tối ưu layer cache backend</code></td></tr>
    <tr><td><code>ci</code></td><td>Sửa GitHub Actions</td><td><code>ci: thêm workflow chạy lint</code></td></tr>
    <tr><td><code>revert</code></td><td>Hoàn tác commit trước</td><td><code>revert: feat(recipes): thêm api tạo công thức</code></td></tr>
  </tbody>
</table>

<h3>Danh sách scope</h3>

<table>
  <thead>
    <tr><th>Scope</th><th>Phạm vi ảnh hưởng</th></tr>
  </thead>
  <tbody>
    <tr><td><code>auth</code></td><td>Xác thực, JWT, Google OAuth, profile</td></tr>
    <tr><td><code>categories</code></td><td>Danh mục công thức</td></tr>
    <tr><td><code>recipes</code></td><td>Công thức, nguyên liệu, các bước</td></tr>
    <tr><td><code>search</code></td><td>Tìm kiếm, lọc, sắp xếp, phân trang</td></tr>
    <tr><td><code>media</code></td><td>Upload ảnh, MinIO</td></tr>
    <tr><td><code>jobs</code></td><td>Background jobs (BullMQ)</td></tr>
    <tr><td><code>shared</code></td><td>Package types dùng chung</td></tr>
    <tr><td><code>backend</code></td><td>Thay đổi chung phía backend</td></tr>
    <tr><td><code>frontend</code></td><td>Thay đổi chung phía frontend</td></tr>
    <tr><td><code>docker</code></td><td>Docker, compose, nginx</td></tr>
    <tr><td><code>deps</code></td><td>Cập nhật dependencies</td></tr>
  </tbody>
</table>

<h3>Quy tắc viết mô tả</h3>

<ul>
  <li>Viết bằng <b>tiếng Việt có dấu</b></li>
  <li>Dùng <b>động từ nguyên thể</b>: "thêm", "sửa", "xóa" — không dùng "đã thêm", "đang sửa"</li>
  <li><b>Không viết hoa</b> chữ cái đầu, <b>không có dấu chấm</b> cuối câu</li>
  <li>Dòng đầu giới hạn <b>72 ký tự</b></li>
  <li>Cần giải thích thêm thì để trống một dòng rồi viết phần body</li>
</ul>

<h3>Ví dụ commit đầy đủ</h3>

<pre><code>feat(auth): thêm cơ chế refresh token rotation

Mỗi lần refresh, token cũ được đánh dấu isRevoked = true và sinh
token mới. Phát hiện reuse attack sẽ ghi log cảnh báo mức WARNING.

Closes #12</code></pre>

<h3>Commit chung nhiều người</h3>

<p>Khi hai người trở lên cùng làm một commit, thêm dòng <code>Co-authored-by</code> ở cuối, cách phần trên <b>hai dòng trống</b>:</p>

<pre><code>feat(recipes): thêm api upload ảnh công thức


Co-authored-by: Trần Minh Tài &lt;2312740@dlu.edu.vn&gt;</code></pre>

<hr/>

<h2>🌿 Quy ước Branch</h2>

<pre><code>&lt;type&gt;/&lt;scope&gt;-&lt;mô-tả-ngắn&gt;</code></pre>

<table>
  <thead>
    <tr><th>Ví dụ</th><th>Ý nghĩa</th></tr>
  </thead>
  <tbody>
    <tr><td><code>feat/auth-google-oauth</code></td><td>Thêm đăng nhập Google</td></tr>
    <tr><td><code>fix/recipes-n-plus-one</code></td><td>Sửa lỗi N+1 query</td></tr>
    <tr><td><code>docs/readme-deployment</code></td><td>Bổ sung hướng dẫn triển khai</td></tr>
  </tbody>
</table>

<ul>
  <li>Dùng <b>chữ thường</b>, không dấu tiếng Việt, ngăn cách bằng dấu gạch ngang</li>
  <li><b>Không commit trực tiếp vào <code>main</code></b> — mọi thay đổi phải qua Pull Request</li>
  <li>Xóa branch sau khi PR đã merge</li>
</ul>

<hr/>

<h2>🔀 Quy ước Pull Request</h2>

<h3>Tiêu đề PR</h3>

<p>Tiêu đề PR <b>bắt buộc</b> theo định dạng:</p>

<pre><code>Tên-MSSV: Title</code></pre>

<table>
  <thead>
    <tr><th>Thành viên</th><th>Tiêu đề PR mẫu</th></tr>
  </thead>
  <tbody>
    <tr><td>Trần Thị Phương Trang</td><td><code>Trang-2314288: Thêm CRUD công thức nấu ăn</code></td></tr>
    <tr><td>Đinh Thị Mai Lành</td><td><code>Lành-2312660: Hoàn thiện Full-Text Search tiếng Việt</code></td></tr>
    <tr><td>Trần Nguyễn Tuấn Anh</td><td><code>TuấnAnh-2312577: Thêm cơ chế refresh token rotation</code></td></tr>
    <tr><td>Trần Minh Tài</td><td><code>Tài-2312740: Tích hợp upload ảnh lên MinIO</code></td></tr>
  </tbody>
</table>

<h3>Mô tả PR</h3>

<p><b>PR không có mô tả sẽ bị đóng.</b> Mô tả phải trả lời được: làm gì, tại sao, và kiểm thử thế nào.</p>

<pre><code>## Mô tả
Ngắn gọn PR này làm gì và giải quyết vấn đề gì.

## Yêu cầu liên quan
- FR-AUTH-004: Làm mới Access Token

## Thay đổi chính
- Thêm RefreshTokenCommand và handler tương ứng
- Cập nhật schema bảng refresh_tokens
- Thêm logic phát hiện reuse attack

## Cách kiểm thử
1. Đăng nhập để lấy cặp token
2. Gọi POST /api/v1/auth/refresh với refresh token
3. Xác nhận token cũ bị revoke, token mới được cấp

## Ảnh chụp màn hình
(Đính kèm nếu có thay đổi giao diện)

## Checklist
- [ ] Code chạy được ở local
- [ ] Đã chạy `pnpm lint` và `pnpm typecheck`
- [ ] Không commit file `.env`
- [ ] Đã tự review lại diff</code></pre>

<h3>Quy tắc review</h3>

<ul>
  <li>Mỗi PR cần <b>ít nhất một approve</b> trước khi merge</li>
  <li>Người phụ trách hạ tầng (<code>FR-AUTH</code> / <code>FR-OBS</code>) review các PR chạm vào <code>packages/shared</code>, <code>docker-compose.yml</code> hoặc cấu hình chung</li>
  <li>PR nên <b>dưới 400 dòng thay đổi</b> — quá lớn thì tách nhỏ</li>
  <li>Merge bằng <b>Squash and merge</b> để giữ lịch sử <code>main</code> gọn</li>
  <li>Người tạo PR chịu trách nhiệm giải quyết conflict trước khi merge</li>
</ul>

<hr/>

<h2>👥 Thành viên nhóm — CTK47A</h2>

<p>Mỗi thành viên phụ trách <b>trọn một khối tính năng</b> — làm đầy đủ từ database, API backend đến giao diện frontend, không chia theo layer.</p>

<div align="center">
<table>
  <thead>
    <tr>
      <th align="center">Avatar</th>
      <th align="center">MSSV</th>
      <th align="center">Họ tên</th>
      <th align="center">GitHub</th>
      <th align="center">Khối phụ trách</th>
      <th align="center">Scope</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td align="center"><img src="https://github.com/ChuChoaChan131019.png" width="50" height="50"/></td>
      <td align="center">2314288</td>
      <td align="center">Trần Thị Phương Trang<br/><sub>🧭 Trưởng nhóm</sub></td>
      <td align="center"><a href="https://github.com/ChuChoaChan131019">@ChuChoaChan131019</a></td>
      <td align="center"><code>FR-RCP-001→007</code> · <code>FR-JOB</code><br/><sub>CRUD công thức, background jobs</sub></td>
      <td align="center"><code>recipes</code><br/><code>jobs</code></td>
    </tr>
    <tr>
      <td align="center"><img src="https://github.com/minnhi09.png" width="50" height="50"/></td>
      <td align="center">2312660</td>
      <td align="center">Đinh Thị Mai Lành</td>
      <td align="center"><a href="https://github.com/minnhi09">@minnhi09</a></td>
      <td align="center"><code>FR-CAT</code> · <code>FR-SRCH</code><br/><sub>Danh mục, tìm kiếm, phân trang</sub></td>
      <td align="center"><code>categories</code><br/><code>search</code></td>
    </tr>
    <tr>
      <td align="center"><img src="https://github.com/dopaemon.png" width="50" height="50"/></td>
      <td align="center">2312577</td>
      <td align="center">Trần Nguyễn Tuấn Anh</td>
      <td align="center"><a href="https://github.com/dopaemon">@dopaemon</a></td>
      <td align="center"><code>FR-AUTH</code> · <code>FR-OBS</code><br/><sub>Xác thực, hạ tầng, CI/CD</sub></td>
      <td align="center"><code>auth</code><br/><code>docker</code></td>
    </tr>
    <tr>
      <td align="center"><img src="https://github.com/minhtai05.png" width="50" height="50"/></td>
      <td align="center">2312740</td>
      <td align="center">Trần Minh Tài</td>
      <td align="center"><a href="https://github.com/minhtai05">@minhtai05</a></td>
      <td align="center"><code>FR-RCP-008,009,010</code> · <code>FR-FILE</code><br/><sub>Upload ảnh, nguyên liệu, các bước</sub></td>
      <td align="center"><code>media</code><br/><code>recipes</code></td>
    </tr>
  </tbody>
</table>
</div>

<p><b>Ghi chú:</b> Việc thêm structured log và trace vào từng module do người phụ trách module đó tự thực hiện, không gom về một người.</p>

<hr/>

<h2>📦 Các module chức năng</h2>

<table>
  <thead>
    <tr><th>Mã</th><th>Module</th><th>Số FR</th><th>Mô tả</th></tr>
  </thead>
  <tbody>
    <tr><td><code>FR-AUTH</code></td><td>Xác thực và người dùng</td><td>7</td><td>Đăng ký, đăng nhập, Google OAuth, refresh token, profile</td></tr>
    <tr><td><code>FR-CAT</code></td><td>Quản lý danh mục</td><td>5</td><td>CRUD danh mục, phân quyền Admin</td></tr>
    <tr><td><code>FR-RCP</code></td><td>Quản lý công thức</td><td>10</td><td>CRUD recipe, publish/archive, ảnh, nguyên liệu, các bước</td></tr>
    <tr><td><code>FR-SRCH</code></td><td>Tìm kiếm và phân trang</td><td>4</td><td>Full-Text Search tiếng Việt, lọc, sắp xếp</td></tr>
    <tr><td><code>FR-FILE</code></td><td>Quản lý tệp tin</td><td>2</td><td>Upload và xóa ảnh trên MinIO</td></tr>
    <tr><td><code>FR-JOB</code></td><td>Background jobs</td><td>3</td><td>Email, sinh thumbnail, sitemap XML</td></tr>
    <tr><td><code>FR-OBS</code></td><td>Quan sát hệ thống</td><td>3</td><td>Health check, structured logging, tracing</td></tr>
  </tbody>
</table>

<h2>🔗 Liên kết</h2>

<ul>
  <li>Source code: <a href="https://github.com/PTUDW-2026-Nhom2/CulinaryBlog">PTUDW-2026-Nhom2/CulinaryBlog</a></li>
  <li>Tổ chức GitHub: <a href="https://github.com/PTUDW-2026-Nhom2">PTUDW-2026-Nhom2</a></li>
</ul>

<hr/>

<div align="center">
  <i>Học phần Phát triển Ứng dụng Web Nâng cao</i>
</div>
