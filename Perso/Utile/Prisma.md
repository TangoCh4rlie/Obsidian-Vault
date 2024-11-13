npm init -y 
npm install typescript ts-node @types/node --save-dev
npx tsc --init
npm install prisma --save-dev
npx prisma init --datasource-provider [le type de bd souhaité]

exemple : 

model User { 
	id Int @id @default(autoincrement()) 
	email String @unique 
	name String? 
	posts Post[] 
} 
model Post { 
	id Int @id @default(autoincrement()) 
	title String 
	content String? 
	published Boolean @default(false) 
	author User @relation(fields: [authorId], references: [id]) 
	authorId Int 
}

npx prisma migrate dev --name init

$$
\int \ln(u) \, \mathrm{d}u = u \ln(u) - u + C
$$


